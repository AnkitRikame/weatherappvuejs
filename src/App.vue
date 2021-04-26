<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp >16 ? 'warm' : ''">
    <main>
      <h3 class="text-center" style="color:#fff; font-size:2.3em; font-weight:bold;"> Weather App</h3>
       
      
       <TabNav :tabs="['WindSpeed','Humidity','Pressure','Sunrise','Sunset']" :selected="selected" @selected="setSelected">
        <Tab :isSelected="selected === 'WindSpeed'">
              <p>{{weather.wind != undefined ? weather.wind.speed : ""}} km/h</p>
              
        </Tab>
        <Tab :isSelected="selected === 'Humidity'">
              <p>{{weather.main != undefined ? weather.main.humidity : ""}} %</p>
        </Tab>
        <Tab :isSelected="selected === 'Pressure'">
           <p>{{weather.main != undefined ? weather.main.pressure : ""}} Pa</p>
          
        </Tab>
        <Tab :isSelected="selected === 'Sunrise'">
           <p>{{dateBuilder()}}</p>
        </Tab>
        <Tab :isSelected="selected === 'Sunset'">
               <p> {{dateBuilder()}}</p>
        </Tab>
      </TabNav>
      

      

      <div class="search-box">
        <input type="text" 
        class="search-bar" 
        placeholder="Search Country here ......."
        v-model="query"
        @keypress="fetchWeather"
        />
        <!-- {{query}} -->
      </div>

      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
            <div class="location">{{ weather.name }}, {{ weather.sys.country}}
            </div>
            <div class="date">
             {{dateBuilder()}}
            </div>
        </div>

        <div class="weather-box">
          <div class="temp">
             {{ Math.round(weather.main.temp) }}°c
          </div>
          <div class="weather">
            {{ weather.weather[0].main }}
          </div>  
        </div>


        <div class="weather-box min_max">
          <div class="weather">
              <p>Max</p>
              {{ Math.round(weather.main.temp_max) }}°c
          </div>  

          <div class="weather">
              <p>Min</p>
              {{ Math.round(weather.main.temp_min) }}°c
          </div> 
        </div>
      
      </div>
      

    </main>

    
  </div>
</template>

<script>

import TabNav from './components/TabNav';
import Tab from './components/Tab';
/* import HelloWorld from './components/HelloWorld.vue' */

export default {
  watch: {
  },
  name: 'App',
  components: {TabNav, Tab},
  data () {
    
    return {
      api_key: 'c101897dbf56f7babf6c6143fa38b723', 
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query:'',
      weather:{},
      selected : 'Wind Speed',
    }
  },
  methods: {
    fetchWeather(e){
      
      if (e.key == "Enter"){
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
        .then(res => {
          return res.json();
        }).then(this.setResults);
      }
   
    },
    setResults(results){
      this.weather = results;
    },

     setSelected(tab) {
        this.selected = tab;
      },

    dateBuilder () {
      let d = new Date();
      let months = ["January","February","March","April","May","June","July","August","September","October","November","December"];
      let days = ["Sunday","Monday","Tuesday","Wednesday","Thursday","Friday","Saturday"];
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();

      return `${day} ${date} ${month} ${year}`;
    }
  }
}
</script>


<style>

*{
  margin:0;
  padding:0;
  box-sizing:border-box;
}

body{
  font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
}

#app{
  background-image: url('./assets/cold.jpg'); 
  background-size:cover;
  object-fit: contain;
  /* background-position: bottom; */
  transition: 0.4s;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#app p{
  margin-top:10px;
  font-size: 23px;
  font-weight: 500;
  color: #30def5;
}

#app.warm{
  background-image: url('./assets/hot.jpg'); 
} 


main{
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(to bottom,rgba(0,0,0,0.25),rgba(0,0,0,0.80));
}

.search-box{
  width: 100%;
  margin-bottom: 30px;
}

.search-box .search-bar{
  display: block;
  width:100%;
  padding: 15px;
  color: #313131;
  font-size:20px;
  appearance: none;
  outline: none;
  background: none;
  box-shadow: 0px 0px 8px rgba(0,0,0,0.25);
  background-color: rgba(255,255,255,0.5);
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s;
}

.search-box .search-bar:focus{
  box-shadow: 0px 0px 16px rgba(0,0,0,0.25);
  background-color: rgba(255,255,255,0.75);
  border-radius: 16px 0px 16px 0px;
}

.location-box .location{
  color: #fff;
  font-size:30px;
  font-weight:500;
  text-align: center;
  text-shadow: 1px 3px rgba(0,0,0,0.25);
}

.location-box .date{
  color: #fff;
  font-size:20px;
  font-weight:300;
  font-style: italic;
  text-align: center;
}

.weather-box{
  text-align: center;
}

.weather-box{
  text-align: center;
}

.weather-box .temp{
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 70px;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0,0,0,0.25);
  background-color: rgba(255,255,255,0.25);
  border-radius: 16px;
  margin: 30px 0px;
  box-shadow: rgba(0,0,0,0.25);
}

.weather-box p{
  font-size: 40px;
  font-weight: 400;
  color: #30def5;
  margin: 10px 40px;
  }

.weather-box .weather{
  color:#fff;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
}

.min_max{
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-content: center;
}


</style>
