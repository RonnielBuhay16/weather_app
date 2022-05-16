<script>
import WeatherInfo from './WeatherInfo.vue'
export default {
  props: {
    temp : Number,
    date : String,
    info : String
  },components: {
      WeatherInfo,
  }
}
</script>

<template>
<br>
<br>
    <div id="slide" :class="temp > 16 ? 'warm' : ''">
        <br>
        <div class="location-box">
          <div class="date">{{ date }}</div>
        </div>
       
    <WeatherInfo 
         v-bind:temp ="temp" />
    </div>
    
</template>
<style>
#slide {
  background-image: url('../assets/cold-bg.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
  height : 200%;
  width: 50%;
  
  
}

#slide.warm {
  background-image: url('../assets/warm-bg.jpg');
}


.location-box .date {
  color: #FFF;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}
</style>