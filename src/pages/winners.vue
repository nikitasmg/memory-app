<template>
  <div class="page">
    <h1 class="title"> Списки победителей</h1>
    <div class="wrapper">
      <ul class="winners">
        <li
          class="winners__item"
          :key="player.username"
          v-for="(player, index) in winnersList"
        > {{index + 1}}.
          {{ player.username }} -
          {{ player.time }}
        </li>
      </ul>

    </div>
    <my-button
    class="btn"
    @click="startNewGame"
    >
      Играть еще
    </my-button>
  </div>

</template>

<script>
import myButton from "~/components/UI/MyButton";
export default {
  components: {myButton},

  data() {
    return {
      winnersList: []
    }
  },
  mounted() {
    this.winnersList = JSON.parse(localStorage.getItem('winnersList'))
  },
  methods: {
    startNewGame() {
      console.log('asda')
      this.$router.replace('/game')
    }
  }
}
</script>

<style scoped lang="scss">
.wrapper {
  display: flex;
  justify-content: center;
}

.winners {
  list-style: none;
  margin-top: 100px;
  margin-bottom: 100px;
  width: 100%;
  &__item {
    color: white;
    font-size: 25px;
    padding: 10px 30px;
    border: 2px solid white;

    &:not(:first-child) {
      border-top:none ;
    }
  }
}
.btn {
  display: block;
  margin: auto;
}
</style>
