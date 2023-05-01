<template>
  <div class="pie">
    Student Enrollment Rates
    <h4> Enter two distinct integers from 1-32, which will represent a unique district in NYC, to compare their student enrollment rates</h4>
    <input type="text" v-model="first" placeholder="Integer 1-32" class="search">
    <input type="text" v-model="second" placeholder="Integer 1-32" class="search">
    <br>
    <button type="button" v-on:click="getChartData(), clearData()">Enter</button>
    <div class="chart">
      <PieChart class="chart" v-if="gotData" :chartData="chartData" :chartOptions="chartOptions" />
    </div>
    <div class="info"></div>
  </div>
  <div></div>
</template>

<script>
import PieChart from '../components/PieChartTemp.vue'
export default {
  name: 'PieChartView',
  components: {
    PieChart
  },
  data() {
    return {
      first: null,
      second: null,
      chartData: {
        labels: [],
        datasets: [{ label: 'Students', data: [] }]
      },
      chartOptions: {
        responsive: true,
        backgroundColor: ['#00FF00', '#FF0000']
      },
      gotData: false
    }
  },
  methods: {
    getChartData: async function () {
      this.gotData = false
      try {
        let districts = []
        let res = await fetch('https://data.cityofnewyork.us/resource/7z8d-msnt.json')
        let data = await res.json()
        console.log(data)
        this.chartOptions.backgroundColor.push('#0000FF', '#FF0000')
        data.forEach((district) => districts.push(district.ytd_enrollment_avg_))
        console.log(districts)
        this.chartData.labels.push(`District ${this.first}`)
        this.chartData.labels.push(`District ${this.second}`)
        this.chartData.datasets[0].data.push(districts[this.first -1])
        this.chartData.datasets[0].data.push(districts[this.second -1])
        this.gotData = true
      } catch (error) {
        console.log(error)
      }
    },
    clearData: function() {
    this.chartData.labels = []
    this.chartData.datasets[0].data = []
    }
  },
 
}
</script>

<style scoped>
.pie {
  text-align: center;
  font-size: 40px;
  color: #ff00ff;
}
.search{
margin: auto 10px;
}
h4 {
  font-size: 20px;
}
</style>
