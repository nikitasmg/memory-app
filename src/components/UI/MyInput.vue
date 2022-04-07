<template>
  <input
    :value="value"
    @input="updateInput"
    class="input"/>
</template>

<script>
export default {
  name: 'MyInput',
  props: {
    value: [String, Number]
  },
  methods: {
    updateInput(event) {
      this.$emit('input', event.target.value)
    }
  },
}
</script>

<style scoped lang="scss">
@import "../../assets/css/variables";

.input {
  padding: 10px 10px;
  background-color: transparent;
  border: 2px solid $brown-minus;
  color: $yellow;
  font-size: 20px;
  transition: all .1s linear;

  &:focus {
    border: 2px solid $yellow;
    outline: none;
    transition: all .1s linear;
  }

  &::placeholder {
    color: $grey;
    opacity: .4;
  }
}

</style>

