<template>
  <div class="page">
    <h1 class="title">Welcome {{ username }}</h1>
    <span class="timer">{{ humanTimer }}</span>
    <div class="card__wrapper">
      <card
        v-for="card in cards"
        :key="card.id"
        @getItem="game(card)"
        :card="card"
      />
    </div>
    <my-button
      class="btn__exit"
      @clickBtn="exit"
    >
      Выйти и завершить
    </my-button>
  </div>
</template>

<script>
import Card from "@/components/UI/Card";
import _isEqual from 'lodash/isEqual'
import MyButton from "@/components/UI/MyButton";

export default {
  components: {MyButton, Card},
  data() {
    return {
      username: '',
      cards: [
        {id: 1, face: "ace", isActive: false, isVisible: true,},
        {id: 3, face: "king", isActive: false, isVisible: true,},
        {id: 4, face: "ten", isActive: false, isVisible: true,},
        {id: 5, face: "dama", isActive: false, isVisible: true,},
        {id: 6, face: "ace", isActive: false, isVisible: true,},
        {id: 7, face: "valet", isActive: false, isVisible: true,},
        {id: 8, face: "king", isActive: false, isVisible: true,},
        {id: 9, face: "dama", isActive: false, isVisible: true,},
        {id: 10, face: "valet", isActive: false, isVisible: true,},
        {id: 11, face: "ten", isActive: false, isVisible: true,},
      ],
      activeCard: null,
      counter: 0,
      isGameStart: false,
    }
  },
  mounted() {
    this.username = localStorage.getItem('username')
  },
  updated() {
    this.stopTimer()
  },
  computed: {
    visibleCards() {
      return this.cards.filter(el => el.isVisible)
    },
    activeCards() {
      return this.cards.filter(el => el.isActive)
    },
    humanTimer() {
      const time = new Date(this.counter * 1000)
      const minutes = time.getMinutes() < 10 ? '0' + time.getMinutes() : time.getMinutes()
      const seconds = time.getSeconds() < 10 ? '0' + time.getSeconds() : time.getSeconds()
      return minutes + ':' + seconds
    }
  },
  methods: {
    game(card) {
      this.startTimer()
      if (this.activeCards.length <= 1) {
        card.isActive = true
        if (this.activeCard?.face === card.face && !_isEqual(this.activeCard, card)) {
          setTimeout(() => {
            this.cards.map(el => {
                if (el.face === card.face) {
                  el.isVisible = false
                  el.isActive = false
                }
              }
            )
          }, 700)
          this.activeCard = null
        } else {
          if (!this.activeCard) {
            this.activeCard = card
          } else if (!_isEqual(this.activeCard, card)) {
            setTimeout(() => {
              this.cards.map(el => el.isActive = false)
            }, 700);
            this.activeCard = null
          }
        }
      }
    },
    exit() {
      this.$router.replace('/')
      localStorage.removeItem('username')
    },
    startTimer() {
      if (!this.isGameStart) {
        this.isGameStart = setInterval(() => {
          this.counter += 1
        }, 1000)
      }
    },
    stopTimer() {
      if (!this.visibleCards.length) {
        clearInterval(this.isGameStart)
        this.setToWinners()
      }
    },
    setToWinners() {
      let winners
      const player = {username: this.username, time: this.humanTimer}
      if (!localStorage.getItem('winnersList')) {
        winners = [player]
      } else {
        winners = JSON.parse(localStorage.getItem('winnersList'))
        const targetPlayer = winners.find(el => el.username === player.username)
        if (targetPlayer) {
          if (targetPlayer.time > player.time) {
            targetPlayer.time = player.time
          }
        } else {
          winners.push(player)
        }
      }
      localStorage.setItem('winnersList', JSON.stringify(winners))
      this.$router.replace('/winners')
    }
  }
}

</script>

<style scoped lang="scss">

.card__wrapper {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 40px;
  margin-top: 100px;
  @media (max-width: 700px) {
    margin-top: 30px;
    gap: 20px;
  }
}

.btn__exit {
  position: absolute;
  top: 10px;
  right: 20px;
  padding: 10px;
  font-size: 15px;

  @media (max-width: 700px) {
    padding: 1px;
    top: 80px;
  }
}

.title {
  @media (max-width: 700px) {
    margin-bottom: 50px;
  }
}

.timer {
  display: block;
  text-align: center;
  font-size: 30px;
  color: white;
  margin-top: 20px;
  @media (max-width: 700px) {
    top: 50px;
  }
}

</style>
