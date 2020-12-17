<template>
    <div id="app">
       <main>
         <div class="search-box">
           <input type="text" v-model="query"  @keypress="fetchWeather" class="search-bar" placeholder="Search country ....." />
         </div> 
         <div class="weather-wrap" v-if="typeof weather.main != 'undefined'" >
           <div class="location-box">
             <div class="location"> {{ weather.name }}, {{ weather.sys.country }} </div>
               <div class="date">
                {{ dateBuilder() }}
             </div>
             <div class="weather-box">
          
                <div class="temp"> {{Math.round(weather.main.temp)}}°C  </div>
                
              <div class="weather"> {{ weather.weather[0].main }}</div>
             </div>
             
           </div>
         </div>
       </main>



    </div>
      
     
</template>

<script>  
export default {

  data () {
      return {
        api_key: 'dd02b2bf922ab260a43f6585545c89bf',
        url_base: 'https://api.openweathermap.org/data/2.5/',
        weather: {},
        query: '',
       
      }
    },   
    methods: {
      fetchWeather (e) {
        if (e.key == "Enter"){
          fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
          .then(res =>{
            return res.json();
          }).then(this.setResults);
        }
      },
      setResults(results) {
        this.weather = results;
      },
      dateBuilder(){
        let today = new Date();
        let months = ["January", "Febuary", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
        let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
        let day = days[today.getDay()];
        let date = today.getDate();
        let month = months[today.getMonth()];
        let year =today.getFullYear();
        let time = today.getHours();
         let time1 = today.getMinutes();
        let time2 = today.getSeconds();
        return `${day} ${date} ${month} ${year}, ${time} : ${time1} : ${time2}`;

      
    }
    }
}
</script>
<style scoped>
*{
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
}
#app{
  background-image: url('../assets/blue.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}
main{
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75));
}
.search-box .search-bar{
  display: block;
  width: 100%;
  padding: 15px;
  color: #313131;
  font-size: 20px;
  appearance: none;
  border: none;
  outline: none;
  background: none;
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.8);
  background-color: rgba(225, 225, 225, 0.5);
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s;
}
.search-box .search-bar:focus {
   box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.16);
   background-color: rgba(225, 225, 225, 0.75);
    border-radius: 16px 0px 16px 0px;
   
}
.location-box .location {
  color: #fff;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}
.location-box .date{
   color: #fff;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}
.weather-box{
  text-align: center;
}
.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 102px;
  font-weight: 900;
  background-color: rgba(255, 255, 255, 0.25);
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  border-radius: 16px;
  margin: 30px 0px;
  box-shadow: rgba(255, 255, 255, 0.25);
}
.weather-box .weather{
  color: #fff;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
   text-shadow: 3px 6px rgba(0, 0, 0, 0.25);

}
</style>
