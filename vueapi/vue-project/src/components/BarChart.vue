<template>
  <Bar
    v-if="gotData"
   id="bar"
    :options="chartOptions"
    :data="chartData"
  />
</template>

<script>
import { Bar } from 'vue-chartjs'
import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js'

ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)

export default {
  name: 'BarChart',
  components: { Bar },
   data() {
  return {
    chartData: {
      labels: [],
      datasets: [
      {label:"Attendance Average Per District", data: [] }],
    },
    chartOptions: {
      responsive: true,
      borderWidth: 3,
      borderColor:["#ff0000","#00FF00","#0000FF",]
     
    },
    gotData: false,
  };
},
mounted() {
  this.getData();
},
methods: {
  getData: async function () {
    this.gotData = false;
    try {
      let res = await fetch(
        "https://data.cityofnewyork.us/resource/7z8d-msnt.json"
      );
      let data = await res.json();
      let districts = []
      data.forEach((district) => {
        districts.push(district.district)
      })
      this.chartData.labels = districts
      let attendanceRate = []
      data.forEach((district) => {
        attendanceRate.push(district.ytd_attendance_avg_)
      })
      this.chartData.datasets[0].data = attendanceRate
      this.gotData = true;
    } catch (error) {
      console.log(error);
    }
  },
},
};
</script>
