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
        let range= [];
        let totalConnections=[40,50,50,50,20];
        
        this.chartData.map((d) => {
            if(!range.includes(d.age)){
                range.push(d.age);
            }
        });

        this.chartData.map((d) => { 
            for(let i=0; i<range.length; i++){ 
                if(range[i] === d.age){
                    totalConnections[i] += 1;
                } 
            }
        });

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