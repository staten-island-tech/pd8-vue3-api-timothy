<script setup>
defineProps({
  msg: {
    type: String,
    required: true
  }
})
</script>

<template>
  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
    <h3>
This website uses data from free APIs from the 
<a href="https://opendata.cityofnewyork.us/data/"> NYC Open Data</a>
website to create multiple charts that easily display that data. The API for this website gets the attendance rate and enrollment rates for NYC schools in each district.
    </h3>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    color: #FF00FF;
    text-align: left;
  }
}
</style>
