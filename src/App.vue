<template>
  <div class="container--centered">
    <form class="form-test" @submit="submit">
      <h1>Code input example</h1>
      <InputPin
        class="input-pin flex-1"
        numeberOfDigits="6"
        v-model="otp"
        border-color="#9CA3AF"
        focused-border-color="#FCD34D"
        border-width="3px"
        radius="250px"
        bg-color="#efefef"
      ></InputPin>
      <div class="code-box">{{ otp }}</div>
    </form>
  </div>
</template>
<script setup lang="ts">
  import { ref } from 'vue'
  /* @ts-ignore */
  import InputPin from './components/InputPin.vue'

  const submit = () => {
    console.log('submitted')
  }

  const otp = ref('')
</script>
<style scoped>
  .container--centered {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    background-color: red;
    width: 100%;
  }

  .form-test {
    flex: 1;
    padding: 0.5rem;
    width: 100%;
    max-width: 100%;
    overflow: hidden;
    margin-left: auto;
    margin-right: auto;
    background-color: aquamarine;
    min-height: 320px;
    display: flex;
    gap: 2rem;
    flex-direction: column;
    align-items: center;
  }

  .code-box {
    background-color: #fff;
    font-size: 3rem;
    padding: 1rem 2rem;
    font-family: 'Courier New', sans-serif;
  }

  .flex-1 {
    width: 100%;
    justify-content: space-around;
  }

  .input-pin {
    max-width: 320px;
    margin-right: auto;
    margin-left: auto;
  }

  @media screen and (min-width: 1024px) {
    .form-test {
      padding: 1rem;
      width: 640px;
    }
  }
</style>
