<script>
import { Doughnut } from "vue-chartjs";
export default {
    extends: Doughnut,
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
    mounted () {
        const os = this.chartData.map(d => d.os);
        const totalConnections = this.chartData.map(d => d.connections);
        //console.log(os,totalConnections);

        this.renderChart({
            labels: os,
            datasets: [{
                label: this.label,
                data: totalConnections,
            }],
        },this.options);
    }
}
</script>