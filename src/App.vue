<template>
  <div id="app">
    <div class="sidebar">
      <div class="title">- Dashbool -</div>
      <div class="avatar">
        <div class="circle"></div>
        <div class="info">
          <p>Welcome</p>
          <p class="name">Mario Rossi</p>
        </div>
      </div>
      <div class="general">GENERAL</div>
      <ul class="list">
        <li>
          <div class="list-head">
            <div>
              <i class="fa fa-home" aria-hidden="true"></i>
              <p>Home</p>
            </div>
            <i
              @click="toggleMenu"
              :class="isOpen ? 'fa fa-chevron-up' : 'fa fa-chevron-down'"
              aria-hidden="true"
            >
            </i>
          </div>
          <ul class="sub-list" :style="isOpen ? ' ' : 'display: none;'">
            <li>Dasboard</li>
            <li>Dasboard</li>
            <li>Dasboard</li>
          </ul>
        </li>
        <li>
          <div class="list-head">
            <div>
              <i class="fa fa-map" aria-hidden="true"></i>
              <p>Maps</p>
            </div>
            <i class="fa fa-chevron-down" aria-hidden="true"></i>
          </div>
          <ul class="sub-list">
            <li>Dasboard</li>
            <li>Dasboard</li>
            <li>Dasboard</li>
          </ul>
        </li>
        <li>
          <div class="list-head">
            <div>
              <i class="fa fa-cog" aria-hidden="true"></i>
              <p>Config</p>
            </div>
            <i class="fa fa-chevron-down" aria-hidden="true"></i>
          </div>
          <ul class="sub-list">
            <li>Dasboard</li>
            <li>Dasboard</li>
            <li>Dasboard</li>
          </ul>
        </li>
        <li>
          <div class="list-head">
            <div>
              <i class="fa fa-envelope" aria-hidden="true"></i>
              <p>Contacts</p>
            </div>
            <i class="fa fa-chevron-down" aria-hidden="true"></i>
          </div>
          <ul class="sub-list">
            <li>Dasboard</li>
            <li>Dasboard</li>
            <li>Dasboard</li>
          </ul>
        </li>
      </ul>
    </div>
    <div class="stage">
      <div class="topbar">
        <i class="fa fa-bars" aria-hidden="true"></i>
        <div>
          <i class="fa fa-envelope-o" aria-hidden="true"></i>
          <div class="circle"></div>
          <p>Mario Rossi</p>
          <i class="fa fa-chevron-down" aria-hidden="true"></i>
        </div>
      </div>
      <div class="main">
        <!-- first line -->
        <div class="chart-box" v-if="monthlyConnections.length > 0">
          <div>Montly Connections</div>
          <line-chart :chartData="monthlyConnections" :options="chartOptions" label="MonthlyConnections"></line-chart>
        </div>
        <!-- second line -->
        <div class="box">
          <div class="half chart-box" v-if="usersAge.length > 0">
            <div>Users Age Range</div>
            <bar-chart :chartData="usersAge" :options="chartOptions"></bar-chart>
          </div>
          <div class="half chart-box" v-if="usersOS.length > 0">
            <div>Operating System</div>
            <doughnut-chart :chartData="usersOS" :options="chartOptions" label="Users' Devices"></doughnut-chart>
          </div>
        </div>
        <!-- third line -->
        <div class="button-play" @click="dataStart">
          <i class="fa fa-play" aria-hidden="true"></i>
        </div>
        <div class="chart-box" v-if="monthlyConnections.length > 0">
          <div>Solar Power</div>
          <solar-chart :chartData="solarPerformance" :options="chartOptions" label="Daily"></solar-chart>
        </div>
        <!-- fourth line -->
        <div class="title">Today</div>
        <div class="box">
          <div class="half chart-box" v-if="today.length > 0">
            <div>Users Age Range</div>
            <bar-chart-today :chartData="today" :options="chartOptions"></bar-chart-today>
          </div>
          <div class="half chart-box" v-if="today.length > 0">
            <div>Operating System</div>
            <doughnut-chart-today :chartData="today" :options="chartOptions" label="Users' Devices"></doughnut-chart-today>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
//import Vue from "vue";
/* eslint-disable */
import axios from "axios";
import LineChart from "./components/LineChart";
import DoughnutChart from "./components/DoughnutChart.vue";
import BarChart from "./components/BarChart.vue";
import SolarChart from "./components/SolarChart";
import BarChartToday from "./components/BarChartToday.vue";
import DoughnutChartToday from "./components/DoughnutChartToday.vue";

export default {
  components: {
    LineChart,
    DoughnutChart,
    BarChart,
    SolarChart,
    BarChartToday,
    DoughnutChartToday
  },
  data() {
    return {
      isOpen: false,
      monthlyConnections: [],
      usersOS: [],
      usersAge: [],
      today: [],
      solarPerformance:[
        {hour: 1,yield: 0,},
        {hour: 2,yield: 0,},
        {hour: 3,yield: 0,},
        {hour: 4,yield: 0,},
        {hour: 5,yield: 0,},
        {hour: 6,yield: 0,},
        {hour: 7,yield: 0,},
        {hour: 8,yield: 0,},
        {hour: 9,yield: 0,},
        {hour: 10,yield: 0,},
        {hour: 11,yield: 0,},
        {hour: 12,yield: 0,},
        {hour: 13,yield: 0,},
        {hour: 14,yield: 0,},
        {hour: 15,yield: 0,},
        {hour: 16,yield: 0,},
        {hour: 17,yield: 0,},
        {hour: 18,yield: 0,},
        {hour: 19,yield: 0,},
        {hour: 20,yield: 0,},
        {hour: 21,yield: 0,},
        {hour: 22,yield: 0,},
        {hour: 23,yield: 0,}],
      solarPerformanceDb: [
        {hour: 1,yield: 5,},
        {hour: 2,yield: 0,},
        {hour: 3,yield: 2,},
        {hour: 4,yield: 1,},
        {hour: 5,yield: 3,},
        {hour: 6,yield: 8,},
        {hour: 7,yield: 22,},
        {hour: 8,yield: 35,},
        {hour: 9,yield: 80,},
        {hour: 10,yield: 95,},
        {hour: 11,yield: 98,},
        {hour: 12,yield: 99,},
        {hour: 13,yield: 97,},
        {hour: 14,yield: 82,},
        {hour: 15,yield: 65,},
        {hour: 16,yield: 40,},
        {hour: 17,yield: 25,},
        {hour: 18,yield: 18,},
        {hour: 19,yield: 5,},
        {hour: 20,yield: 4,},
        {hour: 21,yield: 4,},
        {hour: 22,yield: 1,},
        {hour: 23,yield: 0,},
      ],
      reactiveChartData: null,
      chartOptions:{
        responsive: true,
        maintainAspectRatio: false,
        scales: {
          yAxes: [{
            ticks: {
              beginAtZero: true,
              suggestedMax: 100,
            }
          }]
        }
      },
    };
  },
  async created () {
    axios.get("https://jsonbox.io/box_b8a460940b9a7e686a37/605daf557bdf65001594e5ed")
    .then((res) => {
      this.monthlyConnections = res.data.MonthlyConnections;
      this.usersOS = res.data.Devices;
      this.usersAge = res.data.UsersAgeRange;

      axios.get('https://jsonbox.io/box_69a15712e9a8461a26dc')
        .then((res) => {
            this.today = res.data;
        });
    }).catch((err) => {
      console.error(err);
    });
  },
  computed: {
    getRandomIncl(min,max) {
      min = Math.ceil(min);
      max = Math.floor(max);
      return Math.floor(Math.random() * (max - min + 1)) + min;
    },
  },
  methods: {
    toggleMenu: function () {
      this.isOpen = !this.isOpen;
    },
    dataStart: function () {
        let time = setInterval(()=>{
          if(this.solarPerformanceDb.length != 0){
            let index = 23 - this.solarPerformanceDb.length;
            let sliced = this.solarPerformanceDb.shift();
            let variationPerc = Math.cos( Math.PI * Math.round( Math.random()))*(Math.random() * 5);
            let transitionValue = sliced.yield + variationPerc;

            //casi
            if(transitionValue < 0) {
              sliced.yield = 0;
            }

            if(transitionValue > 100){
              sliced.yield = 100;
            }

            if(transitionValue <= 100 && transitionValue >= 0)
            {
              sliced.yield = transitionValue;
            }
            
            this.solarPerformance.splice(index,1,sliced);
          } else {
            clearInterval(time);
          }
        },1000); 
    }

  },
};
</script>

<style lang="scss">
@import "./scss/commons.scss";
#app {
  width: 100%;
  height: 100%;
  display: flex;
  .sidebar {
    width: $sb-w;
    background-color: $primary-color;
    color: $white;
    padding: 1rem 0.5rem;
    display: flex;
    flex-direction: column;
    .title {
      font-size: 1.2rem;
      font-weight: 700;
      margin-bottom: 1rem;
    }
    .avatar {
      display: flex;
      align-items: center;
      margin-bottom: 1rem;
      .circle {
        width: 3rem;
        height: 3rem;
        border-radius: 50%;
        background-color: $white;
      }
      .info {
        margin-left: 1rem;
        p {
          font-size: 1rem;
        }
        .name {
          font-size: 0.8rem;
          font-weight: 700;
        }
      }
    }
    .general {
      font-size: 1rem;
      font-weight: 700;
      margin-bottom: 1rem;
    }
    .list {
      border-top: 0.2rem solid;
      .list-head {
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding-top: 1rem;
        div {
          display: flex;
          flex-direction: row;
          align-items: center;
          p {
            margin-left: 1rem;
            font-size: 1.2rem;
            font-weight: 300;
          }
        }
      }
      .sub-list {
        margin-top: 0.3rem;
        list-style: none;
        li {
          padding: 0.1rem 0;
          padding-left: 2rem;
          font-size: 0.8rem;
          font-weight: 300;
          &:hover {
            background-color: $secondary-color;
          }
        }
      }
    }
  }
  .stage {
    width: $stage-w;
    background-color: $light-color;
    .topbar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 0 2rem;
      background-color: $lighter-color;
      height: 4rem;
      div {
        display: flex;
        align-items: center;
        justify-content: space-between;
        width: 12rem;
        .circle {
          width: 2rem;
          height: 2rem;
          border-radius: 50%;
          background-color: $white;
        }
      }
    }
    .main {
      padding: 2rem;
      overflow: auto;
      /* display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center; */
      .chart-box {
        background-color: $white;
        border-radius: 1rem;
        padding: 1rem;
        display: flex;
        flex-direction: column;
        align-items: center;
        div {
          width: 100%;
          text-align: center;
          font-size: 1.6rem;
          color: $c-title;
          font-weight: 700;
          border-bottom: 1px solid $lighter-color;
          padding-bottom: 1rem;
        }
      }
      .box {
        margin-top: 2rem;
        display: flex;
        justify-content: space-between;
        .half {
          width: 48%;
        }
      }
      .button-play {
        height: 2rem;
        width: 2rem;
        border-radius: 4px;
        background-color: $white;
        display: flex;
        align-items: center;
        justify-content: center;
        margin: 2rem auto;
      }
      .title {
        display: flex;
        align-items:center;
        justify-content: center;
        width: 10rem;

        border-radius: 0.5rem;
        padding: 1rem;
        margin: 2rem auto;
        background-color: $white;
        color: $primary-color;
        font-size: 2rem;
        font-weight: 500;
      }
    }
  }
}
</style>
