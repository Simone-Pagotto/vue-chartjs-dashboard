<script>
/* eslint-disable */
import { Line, mixins } from "vue-chartjs";//
//const { reactiveProp } = mixins;

export default {
    extends: Line,
    mixins: [mixins.reactiveProp],
    props: {
        label: {
            type: String,
        },
        chartData: {
            type: Array,
        },
        options: {
            type: Object,
        }
    },
    data() {
        return {
            chart:null,
        }
    },
    watch: {
        datasets(newDatasets) {
            console.log(newDatasets);
            this.chart.datasets = newDatasets;
            this.chart.update
        }
    },
    mounted () {
        let hours = this.chartData.map(d => d.hour);
        let performance = this.chartData.map(d => d.yield);
        this.renderChart({
            labels: hours,
            datasets: [{
                label: this.label,
                data: performance,
            }],
        },this.options);
    },
    
}
</script>
