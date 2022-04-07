<template>
  <button class="button" @click="$emit('clickBtn')">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name:'MyButton',

}
</script>

<style scoped lang="scss">
@import "src/assets/css/variables";
.button {
  background: transparent;
  border: 2px solid $yellow;
  padding: 10px 30px;
  color: $yellow;
  font-size: 20px;
  transition:all linear .2s ;
  text-transform: uppercase;
  cursor: pointer;
  &:hover {
    background-color: $yellow;
    color: $white;
    transition:all linear .2s ;
  }
  @media (max-width: 700px) {
    font-size: 15px;
  }
}

</style>
