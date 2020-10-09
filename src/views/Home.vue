<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <div class="row mt-5" v-if="arrDeath.length > 0">
        <div class="col">
        <h2>Deaths in U.S.</h2>
        <line-chart :chartData="arrDeath" :options="chartOptions" label="Deaths" color="#f87979" ></line-chart>
        </div>
    </div>
    <div class="row mt-5" v-if="arrTesting.length > 0">
        <div class="col">
        <h2>Testing With Positive and Negative Results</h2>
        <testing-line-chart :chartData="arrTesting" :options="chartOptions" :label="arrLabels" color="#f99979" ></testing-line-chart>
        </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import moment from 'moment';
import LineChart from '../components/LineChart.vue';
import TestingLineChart from '../components/TestingLineChart.vue'

export default {
  name: 'Home',
  components: {
    LineChart,
    TestingLineChart
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
      },
      loaded: true,
      arrTesting: [],
      arrLabels: []
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

    this.arrTesting.push(this.arrTotalTestResults);
    this.arrTesting.push(this.arrPositive);
    this.arrTesting.push(this.arrNegative);
    this.arrTesting.push(this.arrRecovered);
    this.arrLabels = ['Total Testing', 'Total Positive', 'Total Negative', 'Total Recovered']
    // console.log(this.arrDeath);
  },
  methods: {
    loading: function () {
      if (this.loaded) {
        return true;
      }
    }
  }
}
</script>

<style scoped>
  .home {
    display: flex;
    justify-content: center;
    flex-direction: column;
    padding-left: 200px;
    padding-right: 200px;
  }
</style>
