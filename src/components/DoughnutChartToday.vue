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
        let os= [];
        let totalConnections= [20,55,23,44,33];

        this.chartData.map((d) => {
            if(!os.includes(d.device)){
                os.push(d.device);
            }
        });

        this.chartData.map((d) => { 
            for(let i=0; i<os.length; i++){ 
                if(os[i] === d.device){
                    totalConnections[i] += 1;
                } 
            }
        });

        this.renderChart({
            labels: os,
            datasets: [{
                label: this.label,
                backgroundColor: ['#003f5c','#58508d','#bc5090','#ff6361','#ffa600'],
                data: totalConnections,
            }],
        },this.options);
    }
}
</script>