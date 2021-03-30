<script>
import { Bar } from "vue-chartjs";
export default {
    extends: Bar,
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
        const range = this.chartData.map(d => d.range);
        const totalConnections = this.chartData.map(d => d.connections);

        this.renderChart({
            labels: range,
            datasets: [{
                label: 'User Age Range',
                backgroundColor: ['#003f5c','#58508d','#bc5090','#ff6361','#ffa600'],
                data: totalConnections,
            }],
        },this.options);
    }
}
</script>
