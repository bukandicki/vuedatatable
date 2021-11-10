<template lang="pug">
main#app
  Input.search-box(placeholder="Search", v-model="searchQuery")
    img(role="button", slot="append", :src="searchIcon")
  DataTable(:headers="headers", :items="computeMocks")
    template(v-slot:[`created_at`]="{ item }")
      | {{ new Date(item.created_at).toLocaleString() }}

    template(v-slot:[`units`]="{ item }")
      | {{ parseFloat(item.units) }}

    template(v-slot:[`input`]="{ item }")
      Input(:value="item.units", type="number", min="1")
        span(slot="prepend") Qty
</template>

<script>
import DataTable from "@/components/DataTable";
import Input from "@/components/Input";
import searchIcon from "@/assets/search.svg";
import mockData from "@/mock";

export default {
  name: "App",

  components: { DataTable, Input },

  data: () => ({
    mockData,
    searchIcon,

    searchQuery: "",

    headers: [
      {
        title: "Item Code",
        value: "code",
      },
      {
        title: "Product",
        value: "name",
      },
      {
        title: "Package",
        value: "package",
      },
      {
        title: "Available units",
        value: "units",
      },
      {
        title: "Category",
        value: "category",
      },
      {
        title: "Last updated",
        value: "created_at",
      },
      {
        title: "Edit available quantity",
        value: "input",
      },
    ],
  }),

  computed: {
    computeMocks() {
      return mockData.filter((data) => {
        return ["name", "category", "code"].some((key) => {
          return this.searchQuery
            .toLowerCase()
            .split(" ")
            .every((v) => data[key].toLowerCase().includes(v));
        });
      });
    },
  },
};
</script>

<style lang="sass">
#app
  font-family: "Avenir", Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  color: #2c3e50
  margin-top: 60px

.search-box
  margin-bottom: 20px
</style>
