<template lang="pug">
main#app
  Input(placeholder="Search", v-model="searchQuery")
    span(slot="icon-prepend") a
  DataTable(:headers="headers", :items="computeMocks")
    template(v-slot:[`created_at`]="{ item }")
      | {{ new Date(item.created_at).toLocaleString() }}

    template(v-slot:[`units`]="{ item }")
      | {{ parseFloat(item.units) }}

    template(v-slot:[`input`]="{ item }")
      Input(:value="item.units", type="number", min="1")
</template>

<script>
import DataTable from "./components/DataTable";
import Input from "./components/Input";
import mockData from "@/mock";

export default {
  name: "App",

  components: { DataTable, Input },

  data: () => ({
    mockData,

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

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
