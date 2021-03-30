<script>
/* eslint-disable */
import { Line,mixins } from "vue-chartjs"; 
const {reactiveProp} = mixins;
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
    mounted() {
      this.renderLineChart();
    },
    computed: {
        chartDataReact: function() {
            return this.chartData;
        }
    },
    methods: {
        renderLineChart: function() {
            let hours=[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23];
            let performance=[0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0];
            if(this.chartDataReact.length > 0){
                hours = this.chartDataReact.map(d => d.hour);
                performance = this.chartDataReact.map(d => d.yield);
            }

            this.renderChart({
                labels: hours,
                datasets: [{
                    label: 'Percentage of performance',
                    backgroundColor: ['#003f5c'],
                    data: performance,
                }],
            },this.options); 
        }   
    }, 
    watch: {
        chartDataReact: function() {
            //this.chart.destroy();
            //this.renderChart(this.data, this.options);
            this.renderLineChart();
        }
    }       
}
</script>