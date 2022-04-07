<template>
  <div
    class="card"
    :class="{hidden:!card.isVisible, active:card.isActive}"
    @click="$emit('getItem')"
  >
    <img v-if="card.isActive"
      class="image"
      :src="require(`~/assets/images/${card.face}.png`)"
      alt="card"
    >
  </div>
</template>

<script>
export default {
  props: {
    card: {
      currentView: {
        type: String,
        required: true,
      },
      isActive: {
        type: Boolean
      },
      isVisible: {
        type: Boolean
      }
    }
  },
}
</script>

<style scoped lang="scss">
@import "src/assets/css/variables";

.card {
  display: flex;
  justify-content: center;
  align-items: center;
  color: $black;
  font-size: 20px;
  min-height: 230px;
  padding: 10px;
  border-radius: 10px;
  width:calc(20% - 40px);
  object-fit: cover;
  background-color: $white;
  background-image: url("~/assets/images/back.png");
  background-size: cover;
  background-position: center center;

  @media (max-width: 700px) {
    min-height: 100px;
    width:calc(25% - 20px);
  }

  &.hidden {
    display: none;
  }
  &.active {
    background-image: none;
  }
}

.image {
  width: 100%;
  object-fit: cover;

}
</style>
