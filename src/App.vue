<template>
  <div id="app">
    <input
      type="text"
      class="search"
      v-model="query"
      placeholder="Search for a City..."
      v-on:keyup.enter="getWeather"
    />

    <div class="output" v-if="typeof result.main != 'undefined'">
      <h1>City - {{ result.name }}</h1>
      <p>Weather - {{ result.weather[0].main }}</p>
      <p>Temperature - {{ Math.round(result.main.temp) }}°C</p>
    </div>

    <div class="footer">
      <h4>Made with ❤️, built with vue Source code is available on <a href="https://github.com/Sidhoh/Weather-App">Github</a></h4>
    </div>
  </div>
</template>Delhi

<script>
export default {
  name: "App",
  data() {
    return {
      api_key: APP_KEY,
      query: "",
      response: "https://api.openweathermap.org/data/2.5/",
      result: {},
    };
  },
  methods: {
    getWeather() {
      fetch(
        `${this.response}weather?q=${this.query}&units=metric&APPID=${this.api_key}`
      )
        .then((res) => {
          return res.json();
        })
        .then(this.output);
    },
    output(result) {
      this.result = result;
    },
  },
};
</script>
