<template>
  <form @submit.prevent="setName">
    <label class="label" for="name">Войти в игру</label>
    <my-input
      id="name"
      type="text"
      v-model="username"
      :placeholder="placeholder"
      required
    />
    <my-button
      type="submit"
    >
      Начать
    </my-button>
  </form>
</template>

<script>
import MyButton from '@/components/UI/MyButton'
import MyInput from "@/components/UI/MyInput";

export default {
  components: {
    MyInput,
    MyButton
  },
  props: {},
  data() {
    return {
      placeholder: 'Введите имя',
      username: '',
    }
  },
  methods: {
    setName() {
      localStorage.setItem('username', this.username);
      this.username = ''
      this.$router.push('/game')
    }
  }
}

</script>

<style scoped lang="scss">
@import "src/assets/css/variables";

form {
  display: flex;
  flex-direction: column;
  row-gap: 20px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 50%;
  padding: 25px 50px;
  background-color: $white;
  border-radius: 10px;

  @media (max-width: 700px) {
    width: 100%;
  }
}

.label {
  text-align: center;
  font-size: 20px;
}
</style>
