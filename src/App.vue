<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm' : ''">
    <AppHeader/>
    <main>
      <div id="openweathermap-widget-21"></div>

      <div class="search-box">
        <input 
          type="text" 
          class="search-bar" 
          placeholder="Search..."
          v-model="query"
          @keypress="fetchWeather"
        />
      </div>

      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
         <div>
         <LocationInfo 
         v-bind:name ="weather.name" v-bind:country = "weather.sys.country" v-bind:curr_date = "dateBuilder()" />
       </div>

       <div>
         <WeatherInfo 
         v-bind:temp ="Math.round(weather.main.temp)" v-bind:weather = "weather.weather[0].main" />
       </div>
       <br>
       <div>
       <HeatIndex 
         v-bind:temp ="Math.round(weather.main.feels_like)"/>
       </div>
       <br>
       <WeatherForecast/>
       <div class = "forecast">
         <ForecastByDay 
          v-for="info in daily" :key="info" v-bind:temp="Math.round(info.temp.day)"  v-bind:date = "dateConverter(info.dt)"
        />
       </div>
       
      </div>
       
    </main>
  </div>
</template>

<script>
import AppHeader from './components/AppHeader.vue'
import WeatherInfo from './components/WeatherInfo.vue'
import LocationInfo from './components/LocationInfo.vue'
import WeatherForecast from './components/WeatherForecast.vue'
import ForecastByDay from './components/ForecastByDay.vue'
import HeatIndex from './components/HeatIndex.vue'
export default {
  name: 'app',
  data () {
    return {
      api_key: 'af1ec8913c714d8097f4bff7346bb6ce',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {},
      weather_forecast :  {},
      lon : 0.0,
      lat : 0.0,
      daily : {},
    }
  },
  components :{
    AppHeader,
    WeatherInfo,
    LocationInfo,
    WeatherForecast,
    ForecastByDay,
    HeatIndex
    
  },
  methods: {
    fetchWeather (e) {
      if (e.key == "Enter") {
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
          .then(res => {
            return res.json();
          }).then(this.setResults);
      }
     
    },
    setResults (results) {
      this.weather = results;
     
      this.lon = this.weather.coord.lon;
      this.lat = this.weather.coord.lat;
      
      this.getForecast();
    },
    getForecast () {
     
        fetch(`${this.url_base}onecall?lat=${this.lat}&lon=${this.lon}&exclude=hourly,minutely,alerts&units=metric&appid=${this.api_key}`)
          .then(res => {
            return res.json();
          }).then(this.setForecast);
         
      
    },
    setForecast (results) {
      this.weather_forecast = results;
      this.daily = results.daily;
      console.log(this.daily);
      
     
    },
    dateBuilder () {
      let d = new Date();
      let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];

      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();

      return `${day} ${date} ${month} ${year}`;
    },
    dateConverter(unixTime){
    let date_time = new Date(unixTime*1000);
    let d = new Date(date_time);
      let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];

      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();

      return `${day} ${date} ${month} ${year}`;
  },
  }
  
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'montserrat', sans-serif;
}

#app {
  background-image: url('./assets/cold-bg.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}

#app.warm {
  background-image: url('./assets/warm-bg.jpg');
}

main {
  min-height: 100vh;
  padding: 25px;

  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75));
}

.search-box {
  width: 100%;
  margin-bottom: 30px;
}

.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;
  
  color: #313131;
  font-size: 20px;

  appearance: none;
  border:none;
  outline: none;
  background: none;

  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s;
}

.search-box .search-bar:focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px 0px 16px 0px;
}
.forecast{
 padding-left: 30%;
}

</style>
