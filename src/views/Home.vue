<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <div class="row mt-5" v-if="arrDeath.length > 0">
        <div class="col">
        <h2>Deaths in U.S.</h2>
        <line-chart :chartData="arrDeath" :options="chartOptions" label="Deaths" ></line-chart>
        </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import moment from 'moment';
import LineChart from '../components/LineChart.vue';

export default {
  name: 'Home',
  components: {
    LineChart
  },

  data() {
    return {
      arrDeath: [],
      arrDeathIncrease: [],
      arrTotalTestResults: [],
      arrPositive: [],
      arrNegative: [],
      arrRecovered: [],
      chartOptions: {
        responsive: true,
        maintainAspectRatio: false
      }
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

    // console.log(this.arrDeath);
  }
}
</script>

<style scoped>

</style>
