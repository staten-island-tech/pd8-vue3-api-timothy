<template>
  <div class="container">
    <Bar v-if="loaded" :data="chartData" />
  </div>
</template>

<script>
import { Bar } from 'vue-chartjs'
import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js'

ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)

export default {
  name: 'BarChart',
  components: { Bar },
  data: () => ({
    loaded: false,
    chartData: null
  }),
  async mounted () {
    this.loaded = false

    try {
      const data = await fetch("https://data.cityofnewyork.us/resource/qk7d-gecv.json")
      this.chartdata = data

      this.loaded = true
    } catch (e) {
      console.error(e)
    }
  }
}
</script>
async function getData() {
  const response = await fetch("https://data.cityofnewyork.us/resource/qk7d-gecv.json")
  const data = await response.json()
  console.log(data)
  }