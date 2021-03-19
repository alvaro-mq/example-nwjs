<template>
  <div id="app">
    <otp></otp>
  </div>
</template>

<script>
import Otp from './components/Otp.vue';

export default {
  name: 'App',
  components: {    
    Otp
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
