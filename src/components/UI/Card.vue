<template>
  <div
    class="card"
    :class="{hidden:!card.isVisible, active:card.isActive}"
    @click="$emit('click')"
  >
    <transition
      name="custom-classes-transition"
      enter-active-class="animate__animated animate__flipInY"
      leave-active-class="animate__animated animate__flipOutY"
    >
      <p
        v-if="card.isActive"
        class="emoji"
      >
        {{ card.face }}
      </p>
    </transition>
  </div>
</template>

<script>
import 'animate.css';

export default {
  props: {
    card: {
      currentView: {
        type: String,
        required: true,
      },
      isActive: {
        type: Boolean,
        required: true,
      },
      isVisible: {
        type: Boolean,
        required: true,
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
  border-radius: 15px;
  width: 120px;
  height: 120px;
  object-fit: cover;
  background: $white;
  box-shadow: 0px 5px 10px 2px rgba(34, 60, 80, 0.2);
  transition: all .5s linear;
  @media (max-width: 700px) {
    min-height: auto;
    width: 100px;
    height: 100px;
  }
  @media (max-width: 400px) {
    min-height: auto;
    width: 70px;
    height: 70px;
  }

  &.hidden {
    transition: all .5s linear;
    opacity: 0;
  }

  &.active {
    background-image: none;
  }
}

.emoji {
  font-size: 100px;
  @media (max-width: 700px) {
    font-size: 80px;
  }
  @media (max-width: 400px) {
    font-size: 60px;
  }
}



</style>
