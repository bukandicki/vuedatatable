<template lang="pug">
.input
  .input__wrapper
    .input__icon.input__icon--prepend(v-if="$slots['icon-prepend']")
      slot(name="icon-prepend")

    input.input__field(v-bind="$attrs", v-on="listeners")

    .input__icon.input__icon--append(v-if="$slots['icon-append']")
      slot(name="icon-append")
</template>

<script>
export default {
  name: "Input",

  inheritAttrs: false,

  computed: {
    listeners() {
      return {
        ...this.$listeners,
        input: (event) => {
          this.$emit("input", event.target.value);
        },
      };
    },
  },
};
</script>

<style lang="sass">
.input
  &__wrapper
    display: flex
    align-items: center
  
  &__field
    border: solid 1px #c3c3c3
    font-size: 1rem
    padding: .4rem .8rem

    &:focus
      outline: none
</style>