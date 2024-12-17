<template>
    <div>
      <h1>Weather Forecast</h1>
      <button @click="fetchWeather">Get Weather</button>

      <div v-if="weather">
        <ul>
          <li v-for="(forecast, index) in weather" :key="index">
        {{ forecast.date }}
      </li>
          
        </ul>
      </div>
      
      <p v-if="error" style="color: red;">{{ error }}</p>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        weather: null,
        error: null
      };
    },
    methods: {
      async fetchWeather() {
        try {
          const response = await axios.get('https://localhost:7284/WeatherForecast');
          this.weather = response.data;
          this.error = null;
        } catch (err) {
          this.weather = null;
          this.error = 'Failed to fetch weather data';
        }
      }
    }
  };
  </script>
  
  <style scoped>
  h1 {
    font-size: 2em;
    margin-bottom: 20px;
  }
  button {
    padding: 10px 20px;
    font-size: 16px;
  }
  </style>
  