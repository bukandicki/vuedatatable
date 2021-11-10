<template lang="pug">
.data-table
  .data-table__wrapper
    table.data-table__table
      thead.data-table__header
        tr
          th.data-table__header-item(v-for="header in headers") {{ header.title }}
      tbody.data-table__body
        tr(v-if="!items.length")
          td.data-table__body-item--error(:colspan="headers.length") Data collection not found
        tr(v-for="item in items")
          td.data-table__body-item(v-for="header in headers")
            span(v-if="!$scopedSlots[header.value]") {{ item[header.value] }}
            slot(:name="header.value", :item="item")
</template>

<script>
export default {
  name: "DataTable",

  props: {
    headers: { type: Array, default: () => [] },
    items: { type: Array, default: () => [] },
  },

  created() {
    console.log(this);
  },
};
</script>

<style lang="sass">
.data-table
  width: 100%

  &__table
    width: 100%
    border-collapse: collapse

  &__header
    tr
      background: #f2f2f2

  &__header-item
    text-align: left
    padding: 1rem 1.2rem

  &__body-item
    padding: 1rem 1.2rem
    text-align: left
    border-bottom: solid 1px rgba(0,0,0,.12)

    &--error
      text-align: center
      font-weight: 700
</style>
