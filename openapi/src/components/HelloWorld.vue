<template>
<div>

</div>
  
</template>

<script setup>
import {ref, onMounted} from "vue"
const data = ref('')
async function getData() {
  let res = await fetch('https://data.cityofnewyork.us/resource/qk7d-gecv.json')
  let data2 = await res.json()
  data.value.values = data2.results 
}
onMounted(() => {
  getData()
})
</script>

<style lang="scss" scoped>

</style>