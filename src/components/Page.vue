<template>
  <div class="main" :class="[status.toLowerCase()]">
    <div class="container">
      <div class="leftside">
        <a href="" class="logo">the.weather</a>

        <div class="detailed">
          <div class="detailed-temp"><p>{{ temp }}&#176;</p></div>
          <div class="detailed-info">
            <div class="detailed__info-city">
              <span>{{ city }}</span>
              <p>{{ date }}</p>
            </div>
          </div>
          <div class="detailed-status">
            <i class="fas" :class="'fa-'+[weather.toLowerCase()]"></i>
            {{ status }}
          </div>
        </div>
      </div>
    </div>
    <Aside @getCity="getCityData" :weather__data="info"/>
  </div>
</template>

<script>
import Aside from "@/components/Aside.vue";
import axios from "axios";
export default {
  components: {
    Aside,
  },

  data() {
    return {
      temp: "26",
      info: [],
      city: "Chisinau",
      status: "Sunny",
      date: "",
      dataConv: '',
      weather: 'clear'
    };
  },

  methods: {
    getCityData(cityname) {
      this.city = cityname;
      this.getApiData();
    },
    getApiData() {
      const options = {
        method: "GET",
        url: "https://community-open-weather-map.p.rapidapi.com/weather",
        params: {
          q: this.city,
          units: "metric",
        },
        headers: {
          "x-rapidapi-key":
            "ab877ea744msh16c55ab4946fcadp141696jsne59c5d2442f3",
          "x-rapidapi-host": "community-open-weather-map.p.rapidapi.com",
        },
      };

      axios
        .request(options)
        .then((response) => {
          this.info = response.data;
          this.status = response.data.weather[0].main;
          this.temp = Math.floor(response.data.main.temp);
          switch(this.status){
            case "Clouds":
              this.weather = 'cloud'
              break;
            case "Clear":
              this.weather = 'sun' 
              break;
            case "Rain":
              this.weather = 'cloud-rain' 
              break;
            case "Snow":
              this.weather = 'snowflake'
              break;
            case "Mist":
              this.weather = 'smog'
              break;
            case "Wind":
              this.weather = 'wind'
              break;
          }
        })
        .catch(function (error) {
          console.error(error);
        });
    },
    getDate() {
      let days = [
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
        "Sunday",
      ];
      let months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];
      let date = new Date();
      // let hours = date.getHours();
      // let minutes = date.getMinutes();
      let weekDay = date.getDay().toString();
      let fullYear = date.getFullYear();
      let month = date.getMonth();
      // let formatMin = minutes <= 9 ? "0" + minutes : minutes;
      this.date =
        // hours +
        // ":" +
        // formatMin +
        // " - " +
        days[weekDay -1] +
        ", " +
        date.getDate() +
        " " +
        months[month] +
        ", " +
        fullYear;
    },
  },
  mounted() {
    this.getDate();
    this.getApiData();
  },
};
</script>

<style>
.main {
  width: 100%;
  height: 100vh;
  background-image: url(../assets/main-bg.jpg);
  background-repeat: no-repeat;
  background-position: center left;
  background-size: cover;
  transition: background-image 0.2s ease-in-out;
  position: relative;
}
.main::before{
  position: absolute;
  content: '';
  width:100%;
  height: 100%;
  background: rgba(0,0,0,.5);
  top:0;
  left: 0;
  
}
.container {
  width: 100%;
  max-width: 1370px;
  padding: 0 15px;
  margin: 0 auto;
  position: relative;
  z-index: 1;
}
.leftside {
  width: 100%;
  max-width: 70%;
  padding: 50px 0 100px 0;
      display: flex;
    flex-direction: column;
    justify-content: space-between;
    height: 100vh;
     position: relative;
  z-index: 3;
}
.logo {
  text-decoration: none;
  color: white;
  letter-spacing: 1.2px;
  font-weight: 700;
}
.detailed{
  display: flex;
  align-items: center;
}
.detailed-temp{
  margin:0  25px 0 0 ;
}
.detailed-temp p{
  font-size: 152px;
  color:white;
  line-height: 150px;
  font-weight: 500;
}
.detailed-temp span{
  font-size: 32px;
  color:white;
}
.detailed-info{
  margin:0  25px 0 0 ;
}
.detailed__info-city p{
  color: white;
      font-size: 20px;
      font-weight:200;
}
.detailed__info-city span{
  font-size:56px;
  line-height: 56px;
  color: white;
}
.detailed-status{
  display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    color: white;
    font-size: 22px;
    font-weight: 200;
}
.detailed-status i{
  font-size: 55px;
}
.clouds{
  background-image: url(../assets/clouds.jpg);
  color:black;
}
.clear{
  background-image: url(../assets/clear.jpg);
}
.rain{
  background-image: url(../assets/rain.jpg);
}
.snow{
  background-image: url(../assets/snow.jpg);
}
.mist{
  background-image: url(../assets/mist.jpeg);
}
</style>