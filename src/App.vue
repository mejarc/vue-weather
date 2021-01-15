<template>
  <div id="app">
    <main>
        <div class="search-box">
          <input
            id=""
            name=""
            class="search-bar"
            placeholder="Search places"
            v-model="query"
            @keyup.enter="fetchWeather"
          />
        </div>
        <div class="weather wrap" v-if="typeof weather.main != 'undefined'">
          <div class="location-box">
            <div class="location">
              {{ weather.name }}, {{ weather.sys.country }}
            </div>
            <div class="weather-box">
              <div class="temp">{{ Math.round(weather.main.temp)}}&deg; F</div>
              <div class="weather">{{ weather.weather[0].main }}</div>
            </div>
          </div>
        </div>
    </main>
  </div>
</template>

<script>
export default {
  name: "App",
  data: () => {
    return {
      api_key: 'fc91290abde22dc8debf372be12e713e',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {},
    };
  },
  methods: {
    fetchWeather() {
        fetch(`${this.url_base}/weather?q=${this.query}&units=imperial&APPID=${this.api_key}`)
          .then((response) => {
            return response.json();
          })
          .then(this.setResults);
    },
    setResults(results) {
      this.weather = results;
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: "Montserrat", sans-serif;
  font-size: 100%;
}
main {
  background-image: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0.5) rbga(0, 0, 0, 0.5)
  );
  min-height: 100vh;
  padding: 2rem;
}
.location-box,
.weather-box {
  color: white;
  font-size: 2rem;
  font-weight: 500;
  text-align: center;
  text-shadow: 2px 1px 2px black;
}
.date {
  font-style: italic;
}
.temp {
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  box-shadow: 3px 2px rgba(0, 0, 0, 0.25);
  display: inline-block;
  font-size: 2.5rem;
  font-weight: 900;
  margin: 2rem 0;
  padding: 2rem;
  text-shadow: 1px 1px 1px rgba(0, 0, 0, 0.75);
}
.search-box {
  width: 100%;
  margin-bottom: 2rem;
}

.search-box input {
  border: 1px solid rgba(255, 255, 255, 0.75);
  border-radius: 16px;
  box-shadow: 0 0 8px rgba(0, 0, 0, 0.25);
  appearance: none;
  background: none;
  background-color: rgba(255, 255, 255, 0.25);
  display: block;
  font-size: 1.25rem;
  outline: none;
  padding: 1rem;
  transition: 0.4s;
  width: 100%;
}

.search-box input:focus {
  background-color: rgba(255, 255, 255, 0.75);
  box-shadow: 0 0 16px rgba(0, 0, 0, 0.25);
  border-radius: 0;
}
.weather-box .weather {
  font-style: italic;
}

#app {
  background-image: url("./assets/cold-bg.jpg");
  background-size: cover;
  background-position: bottom;
  transition: 0.6s;
}
</style>
