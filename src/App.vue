<template>
  <div id="app" :class="weather.temperature > 55 ? 'warm' : ''">
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
      </form>
      <div class="weather-wrap" v-if="weather.exists === true">
        <div class="location-container">
          <div class="location-div">
            {{ weather.city }} , {{ weather.country }}
          </div>
          <div class="date">{{ getDate() }}</div>
        </div>
        <div class="weather-container">
          <div class="temp">{{ Math.round(weather.temperature) }}° F</div>
          <div class="weather">{{ weather.conditions }}</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      api_key: "e824bd9b37677b9809c9e3a2ce50bb28",
      base_url: "http://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {
        city: "",
        country: "",
        temperature: "",
        conditions: "",
        exists: false
      }
    };
  },
  methods: {
    getWeather(e) {
      e.preventDefault();
      fetch(
        `${this.base_url}weather?q=${this.query}&units=Imperial&appid=${this.api_key}`
      )
        .then(res => res.json())
        .then(res => {
          this.weather.city = res.name;
          this.weather.country = res.sys.country;
          this.weather.temperature = res.main.temp;
          this.weather.conditions = res.weather[0].main;
        })

        .catch(err => console.log(err));
      this.weather.exists = true;
    },
    getDate() {
      let d = new Date();
      let months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "Septermber",
        "October",
        "November",
        "December"
      ];
      let days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday"
      ];

      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();

      return `${day} ${date} ${month} ${year}`;
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

#app.warm {
  background-image: url("./assets/warm.jpg");
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
  margin-top: 5px;
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
