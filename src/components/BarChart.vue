<script>
import { Bar } from "vue-chartjs";
export default {
    extends: Bar,
    props: {
        chartData: {
            type: Array,
        },
        options: {
            type: Object,
        }
    },
    mounted () {
        const range = this.chartData.map(d => d.range);
        const totalConnections = this.chartData.map(d => d.connections);

        this.renderChart({
            labels: range,
            datasets: [{
                
                data: totalConnections,
            }],
        },this.options);
    }
}
</script>
