
<template lang="html">
    <!--Set of individual svg to display######################################@@@@@@@@@@@@@@@@@@@@@@@@@@@-->
      <div id="svgset">
              <svg class="icon img" v-if="WeatherObj.w_Condi==='Clouds'">
                  <use xlink:href="#cloud" />
                </svg>

                <svg class="icon img" v-else-if="WeatherObj.w_Condi==='Clear'">
                    <use xlink:href="#sun" />
                  </svg>

                <svg class="icon img" v-else-if="WeatherObj.w_Condi==='Rain'">
                      <use xlink:href="#rain" />
                    </svg>

                <svg class="icon img" v-else-if="WeatherObj.w_Condi==='Drizzle'">
                        <use xlink:href="#river" />
                      </svg>

                <svg class="icon img" v-else-if="WeatherObj.w_Condi==='Haze'">
                          <use xlink:href="#sea" />
                        </svg>
      </div>

</template>

<script>
export default {
  name:'svgset',

  props:['WeatherObj']
}

</script>

<style lang="css">

#svgset .img{
  width:300px;
  height:300px;
}
</style>
