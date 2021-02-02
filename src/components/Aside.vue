<template>
  <div class="aside">
    <div class="search">
      <input type="text" placeholder="Search location" v-model="city" />
      <button class="btn" @click.prevent="getCityInput">
        <i class="fas fa-search"></i>
      </button>
    </div>
    <div class="cities-list">
         <h3>History</h3>
      <ul>
        <li v-for="(city, index) in cities" :key="index">
          <span>{{ city }}</span>
        </li>
      </ul>
    </div>
    <div class="details">
      <h3>Detailed information</h3>
      <div class="details__item">
        <div class="details__item-title"><p>Cloudy:</p></div>
        <div class="details__item-value">
          <p>{{weather__data.clouds.all }}%</p>
        </div>
      </div>
      <div class="details__item">
        <div class="details__item-title"><p>Humidity:</p></div>
        <div class="details__item-value">
          <p>{{ weather__data.main.humidity }}%</p>
        </div>
      </div>
      <div class="details__item">
        <div class="details__item-title"><p>Wind:</p></div>
        <div class="details__item-value">
          <p>{{ weather__data.wind.speed }}km/h</p>
        </div>
      </div>
      <div class="details__item">
        <div class="details__item-title"><p>Pressure:</p></div>
        <div class="details__item-value">
          <p>{{ weather__data.main.pressure }}mm</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
props: {
    weather__data :{
        type:Object,
        default(){
            return {}
        }
    }
},
  data() {
    return {
      city: "",
      cities: [],
      info: null,
      cloudy: 0,
      humidity: 0,
      wind: 0,
      rain: 0,
    };
  },
  methods: {
    getCityInput() {
      this.$emit("getCity", this.city);
      this.cities.push(this.city)
       this.city = "";
       if(this.cities.length >= 4){
           this.cities.shift()
       }
    },
  },
};
</script>

<style>
.aside {
  height: 100vh;
  width: 100%;
  max-width: 30%;
  background: rgba(255, 255, 255, 0.15);
  box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
  backdrop-filter: blur(10.5px);
  -webkit-backdrop-filter: blur(10.5px);
  /* border-radius: 10px; */
  position: absolute;
  right: 0;
  top: 0;
  padding-left: 30px;
  z-index: 4;
}
.search input {
  background: transparent;
  width: 100%;
  max-width: 80%;
  border: none;
  border-bottom: 1px solid white;
  padding-right: 20px;
  padding: 15px 10px;
  outline: none;
  height: 40px;
  margin-top: 30px;
  color: white;
  font-weight: 200;
  font-family: "Poppins", sans-serif;
  font-size: 16px;
}
.search input::placeholder {
  color: white;
  font-weight: 200;
}
button.btn {
  width: 70px;
  height: 70px;
  background: #669dc4;
  border: none;
  /* float: right; */
  cursor: pointer;
  position: absolute;
  top: 0;
  right: 0;
}
.btn i {
  width: 40px;
  font-size: 32px;
}
.cities-list {
  padding: 30px 0;

}
.cities-list h3 {
  color: white;
  padding-left: 10px;
  padding-bottom: 30px;
}
.cities-list ul {
  list-style: none;
  padding-left: 10px;
  font-family: "Poppins", sans-serif;

}
.cities-list ul li {
  padding: 15px 0 0 0;
  color: white;
  font-weight: 200;
  transition: 1s all ease-in-out;
}
.cities-list ul li span {
  color: white;
  font-weight: 200;
  text-decoration: none;
}
.cities-list ul li span:hover {
  color: rgb(255, 255, 255);
}
.details h3 {
  color: white;
  padding-left: 10px;
  padding-bottom: 30px;
}
.details__item {
  display: flex;
  width: 100%;
  padding: 0 10px;
  margin: 0 0 15px 0;
}
.details__item-title {
  width: 50%;
}
.details__item-title p {
  color:white;
  font-weight: 400;
}
.details__item-value {
  width: 50%;
  text-align: right;
}
.details__item-value p {
  color: white;
  font-weight: 300;
}
</style>