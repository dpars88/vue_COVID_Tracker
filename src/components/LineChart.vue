<script>
import { Line } from "vue-chartjs";

export default {
  extends: Line,
  props: {
    label: {
      type: String
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
    const dates = this.chartData.map(d => d.date).reverse();
    const totals = this.chartData.map(d => d.total).reverse();
    
    this.renderChart(
      {
      labels: dates,
      datasets: [
          {
            label: this.label,
            data: totals,
            backgroundColor: this.color
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

</style>
