<template>
  <button class="button" @click="$emit('click')">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'MyButton',

}
</script>

<style scoped lang="scss">
@import "src/assets/css/variables";

.button {
  background: transparent;
  border: 2px solid $black;
  padding: 10px 30px;
  color: $black;
  font-size: 20px;
  transition: all linear .2s;
  text-transform: uppercase;
  cursor: pointer;

  &:hover {
    border: 2px solid $yellow;
    color: $yellow;
    transition: all linear .2s;
  }

  @media (max-width: 700px) {
    font-size: 15px;
  }
}

</style>
