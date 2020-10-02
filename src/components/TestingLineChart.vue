<script>
import { Line } from "vue-chartjs";

export default {
  extends: Line,
  props: {
    label: {
      type: Array
    },
    chartData: {
      type: Array,
      default: null
    },
    options: {
      type: Object,
      default: null
    },
    color: {
      type: String
    }
  },
  mounted () {
    const testing = this.chartData[0].map(d => d.total).reverse();
    const pos = this.chartData[1].map(d => d.total).reverse();
    const neg = this.chartData[2].map(d => d.total).reverse();
    const recovered = this.chartData[3].map(d => d.total).reverse();
    const dates = this.chartData[0].map(d => d.date).reverse();
    
    this.renderChart(
      {
      labels: dates,
      datasets: [
          {
            label: this.label[0],
            data: testing,
            borderColor: '#fffb00',
            pointStyle: 'dash'
          },
          {
            label: this.label[1],
            data: pos,
            borderColor: '#ff1c1c',
            pointStyle: 'dash'
          },
          {
            label: this.label[2],
            data: neg,
            borderColor: '#09ff00',
            pointStyle: 'dash'
          },
          {
            label: this.label[3],
            data: recovered,
            borderColor: '#0004ff',
            pointStyle: 'dash'
          }
        ]
      },
      this.options
    );
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
    color: #fffb00;
}
</style>