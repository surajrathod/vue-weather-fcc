<template lang="html">
  <div class="footer-info">
    <div class="info info1">
      <svg class="icon info-img" >
          <use xlink:href="#sea" />
        </svg>
      <h3>{{WeatherObj.humidity}} %</h3>
    </div>
    <div class="info info2">
      <svg class="icon info-img" >
          <use xlink:href="#sky" />
        </svg>
        <h3>{{WeatherObj.pressure}} hpa</h3>
    </div>
  </div>
</template>

<script>
export default {
  name:'footer-info',
  props:['WeatherObj']
}
</script>

<style lang="css">
</style>
