<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp >16 ?'warm' : '' ">
    <main>

      <div class="search-box">
         <h1 class="header">Weather Application</h1>
        <input type="text" class="search-bar" placeholder="Search...." v-model="query" @keypress="fetchweather" />
      </div>
      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">{{weather.name}},{{weather.sys.country}}</div>
          <div class="date">{{datebuilder()}}</div>
        </div>
        <div class="weather-box">
          <div class="temp">{{Math.round(weather.main.temp)}}° C</div>
          <div class="weather">{{weather.weather[0].main}}</div>
        </div>
      </div>
    </main>
    
  </div>
</template>

<script>


export default {
  name: 'App',
  data(){
    return{
      api_key:'ae5e27327050221ef31a57c6075df3c2',
      url_base:'https://api.openweathermap.org/data/2.5/',
      query:'',
      weather:{ }

    }
    
  },
  methods: {
      fetchweather(e){
        if(e.key =="Enter")
        {
          fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
          .then(res =>{
            return res.json();
          }).then(this.setresults);
        }

      },
      setresults(results){
        this.weather = results;
      },
      datebuilder(){
        let d = new Date();
        let months = [ "January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];

    let days =["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday","Saturday"];
    let day=days[d.getDay()];
    let date =d.getDate();
    let month = months[d.getMonth()];
    let year =d.getFullYear();
    return `${day} ${date} ${month} ${year}`
        
      }

    }
  
}
</script>

<style>
*{
  margin:0;
  padding: 0;
  box-sizing: border-box;
}
body{
  font-family:'montserrat',sans-serif;
}
#app{
  background-image: url('./assets/drop-3065629_1920.jpg');
  background-size:cover;
  background-position:center;
  transition: 0.8s;
}
#app.warm{
  background-image: url('./assets/photo-1555991653-41533844cda5.jpg');
  
}
main{
  min-height: 100vh;
  padding: 25px;
  
}
.search-box{
  width: 100%;
  margin-bottom: 30px;

}
.search-box .search-bar{
  display: block;
  width: 100%;
  padding: 15px;
  color: rgb(34, 3, 3);
  font-size: 40px;
  appearance: none;
  border: none;
  outline: none;
  background-color: rgba(255,255,255, 0.5);
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s;
}

.search-box .search-bar:focus{

  box-shadow: 0px 0px 16px rgba(0,0,0,0.25);
  background-color: rgba(46, 44, 44, 0.25);
   border-radius: 0px 16px 0px 16px;
   color: white;
}

.location-box , location{
  color: white;
  font-size: 35px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0,0,0, 0.35);

}
.location-box .date{
  color: white;
  font-size: 23px;
  font-weight: 300;
  text-align: center;
  font-style: italic;

}

.weather-box{
  text-align: center;
}
.weather-box .temp{
  display: inline-block;
  padding: 10px 25px;
  color:white;
  font-size: 102px;
  font-weight:900;
  text-shadow: 3px 6px rgba(0,0,0,0.25);
  background-color: rgba(65, 52, 52, 0.5);
  border-radius: 17px;
  margin:30px 0px;
  box-shadow: 3px 6px rgba(0,0,0,0.25);
}
.weather-box .weather{
  color: white;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0,0,0,0.25);
}
.header{
  text-align: center;
  color: white;
  font-size: 40px;
  background-color: rgb(53, 56, 59);
}
</style>
