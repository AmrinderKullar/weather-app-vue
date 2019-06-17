<template>
  <div v-if="isLoading">Loading...</div>
  <div v-else class="home-container">
    <img
      :src="weatherImage"
      alt="weather static image"
      class="weather-bg-image"
    />
    <div class="weather-information-container">
      <div class="weather-information-wrapper">
        <div class="weather-info-location"><span>{{ weatherCity }}, {{ weatherCountry }}</span></div>
        <div class="weather-info-temprature"><span>{{ weatherTemp }}&#176;</span></div>
        <img :src="weatherIcon" alt="weather icon" class="weather-info-icon" />
        <div class="weather-info-name">{{ weatherName }}</div>
      </div>
    </div>
  </div>
</template>

<script>
  import { weatherIcons } from '../utils/constants';

  export default {
    name: 'homeContainer',
    async created() {
      let response = undefined;
      let ipData = undefined;
      ipData = await fetch('http://ip-api.com/json/').then(function(response) { return response.json(); });
      if (ipData) {
        response = await fetch(`http://api.openweathermap.org/data/2.5/weather?q=${ipData.city},${ipData.countryCode}&appid=e557cbd1d9d1c1ea949df32b5db2560d`)
        .then(function(response) {
          return response.json();
        });
        if (response) {
          this.weatherIcon = weatherIcons[response.weather[0].main];
          this.weatherImage = `https://source.unsplash.com/1600x900/?${response.weather[0].main}`;
          this.weatherTemp = (response.main.temp - 273.15).toFixed(1);
          this.weatherCity = response.name;
          this.weatherCountry = response.sys.country;
          this.isLoading = false;
          this.weatherName = response.weather[0].main
        }
      }
    },
    data: function() {
      return {
        isLoading: true,
        weatherIcon: '',
        weatherImage: '',
        weatherTemp: 0,
        weatherCity: '',
        weatherCountry: '',
        weatherName: '',
      };
    },
  }
</script>

<style>
  .weather-bg-image {
    position: fixed;
    right: 0;
    bottom: 0;
    min-width: 100%;
    min-height: 100%;
    z-index: -1;
  }
  .weather-information-container {
    height: 100vh;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    /* background-color: #ffffff61; */
  }
  .weather-information-wrapper {
    background-color: #eeeeeec2;
    padding: 100px 150px;
  }
  .weather-info-location {
    font-size: 32px;
    font-weight: 400;
  }
  .weather-info-temprature {
    font-size: 20px;
    font-weight: 700;
    padding: 10px 0px 25px;
    text-align: center;
  }
  .weather-info-icon {
    display: block;
    margin: 0 auto;
    width: 50px;
  }
  .weather-info-name {
    text-align: center;
    font-size: 16px;
    font-weight: 300;
    margin-top: 10px;
  }
</style>