<script>
import { Line } from "vue-chartjs";
export default {
    extends: Line,
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
        const months = this.chartData.map(d => d.month);
        const totalConnections = this.chartData.map(d => d.connections);

        this.renderChart({
            labels: months,
            datasets: [{
                label: this.label,
                backgroundColor: ['#58508d'],
                data: totalConnections,
            }],
        },this.options);
    }
}
</script>
