<template>
  <div class="pie"> Student Enrollment Rates
<h2> District 1 vs District 31</h2>
    <div class="title">

    </div>
    <div class="main">
     
      </div>
      <div class="chart">
        <PieChart
          class="chart"
          v-if="gotData"
          :chartData="chartData"
          :chartOptions="chartOptions"
        />
      </div>
      <div class="info">
      </div>
    </div>
    <div>
      
    </div>
</template>

<script>
import PieChart from "../components/PieChartTemp.vue";
export default {
  name: "PieChartView",
  components: {
    PieChart,
  },
  data() {
    return {
      chartData: {
        labels: [],
        datasets: [{label: "Students", data: [] }],
      },
      chartOptions: {
        responsive: true,
        backgroundColor: ["#00FF00", "#FF0000"],
      },
      gotData: false,
    };
  },
  mounted() {
    this.getChartData();
  },
  methods: {
    getChartData: async function () {
      this.gotData = false;
      try {
        let districts = []
        let res = await fetch(
          "https://data.cityofnewyork.us/resource/7z8d-msnt.json"
        );
        let data = await res.json();
        console.log(data)
        this.chartOptions.backgroundColor.push("#0000FF", "#FF0000");
        data.forEach((district) => 
        districts.push(district.ytd_enrollment_avg_)
        )
        console.log(districts)
        this.chartData.labels.push("District 1")
        this.chartData.labels.push("District 31")
        this.chartData.datasets[0].data.push(districts[0])
        this.chartData.datasets[0].data.push(districts[30])
        this.gotData = true;
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>


<style>
h2 {
  font-size: 30px;
}

.pie {
  text-align: center;
  font-size: 35px;
}

</style>