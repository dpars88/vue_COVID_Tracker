<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <Main msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import axios from 'axios';
import Main from '../components/Main.vue'

export default {
  name: 'Home',
  components: {
    Main
  },
  async created() {
    const { data } = await axios.get(`https://api.covidtracking.com/v1/us/daily.json`)
    console.log(data);
  }
}
</script>

<style scoped>

</style>
