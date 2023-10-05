<template>
  <div class="container--centered">
    <form class="form-test" @submit="submit">
      <h1>Code input example</h1>
      <InputPin
          numeberOfDigits="6"
          v-model="otp"
          border-color="#9CA3AF"
          focused-border-color="#FCD34D"
          border-width="4px"
          radius="12px"
          bg-color="#efefef"
      ></InputPin>
      <div class="code-box">{{otp}}</div>
    </form>
  </div>
</template>
<script setup lang="ts">
import {ref} from 'vue'
import InputPin from './components/InputPin.vue'
const submit = () => {
  console.log('submitted')
}

const otp = ref('');

</script>
<style scoped>
.container--centered {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  width: 100%;
}

.form-test {
  padding: 1rem;
  width: 100%;
  max-width: 640px;
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
  font-family: "Courier New", sans-serif;
}

</style>
