<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <Main msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import axios from 'axios';
import Main from '../components/Main.vue';
import moment from 'moment';

export default {
  name: 'Home',
  components: {
    Main
  },
  data() {
    return {
      arrDeath: [],
      arrDeathIncrease: [],
      arrTotalTestResults: [],
      arrPositive: [],
      arrNegative: [],
      arrRecovered: []
    }
  },
  async created() {
    const { data } = await axios.get(`https://api.covidtracking.com/v1/us/daily.json`)
    //console.log(data);

    data.forEach(d => {
      const date = moment(d.date, "YYYYMMDD").format("MMDD");

      const {
        death,
        deathIncrease,
        totalTestResults,
        positive,
        negative,
        recovered
      } = d;

      this.arrDeath.push({date, total: death});
      this.arrDeathIncrease.push({date, total: deathIncrease});
      this.arrTotalTestResults.push({date, total: totalTestResults});
      this.arrPositive.push({date, total: positive});
      this.arrNegative.push({date, total: negative});
      this.arrRecovered.push({date, total: recovered});

    });

    //console.log(this.arrDeath);
  }
}
</script>

<style scoped>

</style>
