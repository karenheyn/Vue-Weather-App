<template>
  <div id="app">
    <main>
      <form
        type="submit"
        action="submit"
        class="search-container"
        @submit="getWeather"
      >
        <input
          type="text"
          class="search-bar"
          placeholder="Search..."
          v-model="query"
        />
        {{ query }}
      </form>
      <div class="weather-wrap"></div>
      <div class="location-container">
        <div class="location-div">Manassas, Va</div>
        <div class="date">Wednesday 20 April 2020</div>
      </div>
      <div class="weather-container">
        <div class="temp">70° F</div>
        <div class="weather">Rain</div>
      </div>
    </main>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",
  data() {
    return {
      api_key: "56d8665da94e425b19bae655a790938a",
      base_url: "api.openweathermap.org/data/2.5/",
      query: "",
      weather: {}
    };
  },
  methods: {
    getWeather(e) {
      e.preventDefault();
      if (e.key === "Enter") {
        axios
          .get(`${this.base_url}weather?q=${this.query}&APPID=${this.api_key}`)
          .then(res => res.json())
          .then(res => (this.weather = res))
          .catch(err => console.log(err));
      }
    }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  background-image: url("./assets/cold-grey.jpg");
  background-size: cover;
  background-position: center;
  min-height: 400ms;
}

main {
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75));
}

.search-container {
  width: 100%;
  margin-bottom: 30px;
}

.search-container .search-bar {
  display: block;
  width: 100%;
  padding: 15px;
  color: #313131;
  font-size: 20px;
  appearance: none;
  border: none;
  outline: none;
  background: none;
  background-color: rgba(255, 255, 255, 0.5);
  transition: 400ms;
  box-shadow: 0 0 8px rgba(0, 0, 0, 0.25);
}

.search-container .search-bar:focus {
  background-color: rgba(255, 255, 255, 0.75);
  box-shadow: 0 0 16px rgba(0, 0, 0, 0.75);
}

.location-container .location-div {
  color: #fff;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: -1px 2px rgba(0, 0, 0, 0.25);
}

.location-container .date {
  color: #fff;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
  text-shadow: -1px 2px rgba(0, 0, 0, 0.25);
}
.weather-container {
  text-align: center;
}
.weather-container .temp {
  display: inline-block;
  padding: 10px 0;
  font-size: 85px;
  color: #fff;
  font-weight: 800;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  margin: 30px 0;
}

.weather-container .weather {
  color: #ffffff;
  font-size: 48px;
  font-weight: 600;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>
