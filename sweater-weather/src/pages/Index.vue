<template>
  <q-page class="flex column">
    <div class="col q-pt-lg q-px-md">
      <q-input class="fontColor" v-model="search" placeholder="Search" borderless dark>
        <template v-slot:before>
          <q-icon name="my_location" @click="findLocation" />
        </template>
        <template v-slot:hint>Field hint</template>

        <template v-slot:append>
          <q-btn round dense flat icon="search" />
        </template>
      </q-input>
    </div>

    <template v-if="weatherData">
      <div class="col text-white text-center">
        <div class="text-h4 text-weight-light">{{this.weatherData.name}}</div>
        <div class="text-h6 text-weight-light">{{this.weatherData.weather[0].main}}</div>
        <div class="text-h1 text-weight-thin q-my-lg relative-position">
          <span>{{parseInt(this.weatherData.main.temp)}}</span>
          <span class="text-h4 relative-position degrees">&deg;</span>
        </div>
      </div>
      <div class="col text-center">
        <img src="https://www.fillmurray.com/100/100" alt="Billy" />
      </div>
    </template>
    <template v-else>
      <div class="col column text-center text-white">
        <div class="col text-h2 text-weight-thin">
          Sweater
          <br />Weather
        </div>
        <q-btn
          icon="where_to_vote"
          label="Launch My Weather Balloon"
          flat
          @click="findLocation"
          class="col"
        />
      </div>
    </template>
    <div class="col explore"></div>
  </q-page>
</template>

<script>
export default {
  name: "PageIndex",
  data() {
    return {
      search: "",
      weatherData: null,
      lat: null,
      long: null,
      apiUrl: "https://api.openweathermap.org/data/2.5/weather",
      apiKey: process.env.API_Key
    };
  },
  methods: {
    findLocation() {
      console.log("getLocation");
      navigator.geolocation.getCurrentPosition(position => {
        console.log("position :>> ", position);
        this.lat = position.coords.latitude;
        this.long = position.coords.longitude;
        this.getWeather();
      });
    },
    getWeather() {
      let url = "https://api.openweathermap.org/data/2.5/weather";

      this.$axios(
        `${url}?lat=${this.lat}&lon=${this.long}&appid=${this.apiKey}&units=Imperial`
      ).then(response => {
        this.weatherData = response.data;
        console.log("response :>> ", this.weatherData);

      });
      // api.openweathermap.org/data/2.5/weather?lat={lat}&lon={lon}&appid={your api key}
    }
  }
};
</script>
<style lang="sass">
.q-page
  background: linear-gradient(to bottom, #000428, #004e92)
  .fontColor
    color: white
  .degrees
    top: -42px
  .explore
    flex: 0 0 100px
    background: url(../statics/nyc2.png)
    background-size: contain
    background-position: center bottom
</style>