<template>
  <div id="app">



    <!--Svg Loading
  +++++++++++++++++++++++++++
!!!!!!!!!!!!!!!!!!!!!!!!!!!!
@@@@@@@@@@@@@@@@@@@@@@@@@@@@-->
<svgset></svgset>
    <!--Svg Loading end
  +++++++++++++++++++++++++++
  !!!!!!!!!!!!!!!!!!!!!!!!!!!!
  @@@@@@@@@@@@@@@@@@@@@@@@@@@@-->



      <div class="column column-left">

        <div class="temp">
          <h1 v-if="scale==='F'">{{toFarn()}}<sup>o</sup></h1>
          <h1 v-else>{{toDeg()}}<sup>o</sup></h1>
          <button type="button" name="button" v-on:click="change_scale">{{scale}}</button>
        </div>
          <h4>{{weatherobj.w_Condi}}</h4>
          <h3 class='text'>{{searchtext}}</h3>

      </div>

      <div class="column column-right">

          <input type="text" name="" value="" class='searchbox' placeholder="search here" v-model.lazy="searchtext" v-on:keyup.enter="change_Loca">

          <!--########################Individual svg set loading@@@@@@@@@@@@@@@@-->
          <svgind v-bind:WeatherObj="weatherobj"></svgind>

          <footerinfo v-bind:WeatherObj="weatherobj"></footerinfo>

      </div>
</div>
</template>

<script>
import svgset from './components/svg.vue'
import svgind from './components/svgind.vue'
import footerinfo from './components/footerinfo.vue'

export default {
  name:'app',
  components:{
    svgset,
    svgind,
    footerinfo
  },
  data(){
    return{
    searchtext:'Akola',
    Apikey:'8a3f972c527e83479ac1e553f495f1f0',
    scale:'F',
    weatherobj:{
    temp_K:'',
    humidity:'',
    pressure:'',
    w_Condi:''
}
  }
},
created(){
  this.apiCall();

},

methods:{
  apiCall:function(){
    this.$http.get('http://api.openweathermap.org/data/2.5/weather?q='+this.searchtext+'&APPID='+this.Apikey)
    .then((resp)=>{
      console.log(resp.body.weather[0].main.toString());
       var weatherbody=resp.body;
       return weatherbody;
    })
    .then((weatherbody)=>{
        this.weatherobj.temp_K=weatherbody.main.temp;
        this.weatherobj.humidity=weatherbody.main.humidity;
        this.weatherobj.pressure=weatherbody.main.pressure;
        this.weatherobj.w_Condi=weatherbody.weather[0].main.toString();
    })
  },
  toFarn:function(){
    return ((1.8*(this.weatherobj.temp_K - 273)+32)).toPrecision(2);
  },
  toDeg:function(){
    return (this.weatherobj.temp_K -273.15).toPrecision(2);
  },
  change_scale:function(){
    if(this.scale==='F'){
      this.toDeg();
    this.scale='C';
  }else{
    this.toFarn();
    this.scale='F';
  }
},
  change_Loca:function(){
    this.apiCall();
  }
}

}
</script>

<style>

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  width:800px;
  height:400px;
  background-color:#fefefe;
  margin:200px auto;
  box-shadow:0px 0px 30px -12px black;
  display: flex;
  position: relative;
}
.column{
  display: flex;
  width:400px;
}
.column-left{
  flex-direction: column;
  background-color: #D4D4D4;
}
.column-right{
  flex-direction: column;
}

.temp{
  display: flex;
  justify-content:space-around;

}
.searchbox{
  position: absolute;
  left:36%;
  top:18px;
  height:35px;
  background-color: #D4D4D4;
  border:none;
  text-align: center;
  letter-spacing: 1px;
  font-size:17px;
}
.searchbox:hover,.searchbox:focus{
  border-bottom:2px solid white;
  outline: none;
}
.info{
  display: flex;

}
.info h3{
  line-height:60px;
}
.info-img{
  width:100px;
  height:100px;
  padding-right: 10px;
}
.footer-info{
  background-color: #8870FF;
  display:flex;
  justify-content: space-around;
  color:white;

}
.temp button{
  align-self: center;
  width:54px;
  height:36px;
  border: none;
  background-color: #fefefe;
  font-weight: bold;
}
button:hover{
  background-color:  #D4D4D4;
  border:1px solid white;
}
h4{
  align-self: center;
  margin:0px;
}
.text{
  align-self: center;
  font-size:3rem;
}
body{
  background-color:#dbdbc8;
}

h1, h2 {
  font-size:7rem;
}

</style>
