<script>
import { Line,mixins } from "vue-chartjs";//
const { reactiveProp } = mixins;

export default {
    extends: Line,
    mixins: [reactiveProp],
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
        let hours=[];
        let performance=[];
        console.log(this.chartData);
        if(this.chartData.length > 0){
            
            hours = this.chartData.map(d => d.hour);
            performance = this.chartData.map(d => d.yield);
        }
        

        this.renderChart({
            labels: hours,
            datasets: [{
                data: performance,
            }],
        },this.options);
    }
}
</script>
