<template lang="pug">
.input
  .input__wrapper
    .input--prepend(v-if="$slots['prepend']")
      slot(name="prepend")

    input.input__field(v-bind="$attrs", v-on="listeners")

    .input--append(v-if="$slots['append']")
      slot(name="append")
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

  &--append,
  &--prepend
    padding: .4rem .8rem
    border: solid 1px #c3c3c3
  

  &--append
    border-left: unset
    
  &--prepend
    border-right: unset
    background: #f2f2f2
</style>