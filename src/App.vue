<template>
  <div class="hello">
    <button @click="fetchData">Click Me!</button>
    <div v-if="weather">
      <p>{{ weather.main }}</p>
      <p> {{ weather.description }}</p>
    </div>

  </div>
</template>
<script>
export default {
  props: {
    msg: String,
  },
  data() {
    return {
      weather: {},
      apiKey: import.meta.env.VITE_apikey
    };
  },
  methods: {
    fetchData() {
      const urlBase = "https://api.openweathermap.org/data/2.5/weather";
      let location = "barcelona"
      const url = `${urlBase}?q=${location}&appid=${this.apiKey}&units=metric&lang=ES`;
      console.log(url);
      fetch(url)
        .then( (response) => {
          response.json()
          .then( (data) => {
            this.weather = data.weather[0];
            console.log(this.weather)
          });
        }).catch( (err)=> {
          this.error(err);
          console.error(err);
        });
    },
  },
};
</script>
<style>
button {
padding: 12px 32px;
font-size: 16px;
border-radius: 8px;
}
</style>