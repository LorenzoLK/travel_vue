<template>
  <div>
    <main>
      <div class="search-box">
        <span class="title title-word-1">Flights </span> 
        <span class="title title-word-2">Around </span>
        <span class="title title-word-3">The </span>
        <span class="title title-word-4">World</span>
        <input 
          type="text" 
          class="search-bar" 
          placeholder="Departing country, city, or airport"
          v-model="query_depart_loc"
          @keypress="fetchInfo"
        />

        <input 
          type="text" 
          class="search-bar" 
          placeholder="When will you depart?"
          v-model="query_depart_date"
          @keypress="fetchInfo"
        />

      </div>
      <div class="search-box">
        <input 
          type="text" 
          class="search-bar" 
          placeholder="Arriving country, city, or airport"
          v-model="query_arrive_loc"
          @keypress="fetchInfo"
        />

        <input 
          type="text" 
          class="search-bar" 
          placeholder="When will you arrive?"
          v-model="query_arrive_date"
          @keypress="fetchInfo"
        />
      </div>

      <div class="'flight-info" v-if="typeof travel.main != 'undefined'">
        <div class="location-hub">
          <div class="">{{ travel.name }}</div>
          <div class="">{{ Math.round(travel.main.currency) }}°F</div>
        </div>
      </div>

      <div class='weather-info' v-if="typeof weather.main != 'undefined'">
        <div class="location-hub">
          <div class="">{{ weather.name }}</div>
          <div class="">{{ Math.round(weather.main.temp) }}°F</div>
        </div>
      </div>

    </main>
  </div>
</template>

<script>

export default {
  name: 'App',
  data () {
    return {
        weather_api_key: '938b78026546140d37edf372f2b40f89',
        travel_api_key: 'd054f71cacmsh045112f43332108p1229fejsn8281182815f5',
        weather_url_base: 'https://api.openweathermap.org/data/2.5/',
        travel_url_base: 'https://partners.api.skyscanner.net/apiservices/browsequotes/v1.0/US/USD/en-US/',
        query_depart_loc: '',
        query_arrive_loc: '',
        query_depart_date: '',
        query_arrive_date: '',
        weather: {},
        travel: {}
    }
  },
  methods: {
    async fetchInfo(e) {
      if (e.key == 'Enter'){
        let response = await fetch(`${this.weather_url_base}weather?q=${this.query_depart}&units=imperial&APPID=${this.weather_api_key}`);
        let json= await response.json();
        this.weather = await json;

        let travelRes = await fetch(`${this.travel_url_base}travel?q=${this.query_depart_loc}/
          ${this.query_depart_loc}/
          ${this.query_arrive_loc}/${this.query_depart_date}/
          ${this.query_arrive_date}`);
        let travelJSON = await travelRes.json();
        this.travel = await travelJSON;
      }
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  background-color:aquamarine;
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}

main {
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.25));
}

.title {
  font-size: 102px;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  animation: color-animation 10s linear infinite;
}

.title-word-1 {
  --color-1: #DF8453;
  --color-2: #3D8DAE;
  --color-3: #E4A9A8;
}

.title-word-2 {
  --color-1: #DBAD4A;
  --color-2: #ACCFCB;
  --color-3: #17494D;
}

.title-word-3 {
  --color-1: #ACCFCB;
  --color-2: #E4A9A8;
  --color-3: #ACCFCB;
}

.title-word-4 {
  --color-1: #3D8DAE;
  --color-2: #DF8453;
  --color-3: #E4A9A8;
}

@keyframes color-animation {
  0%    {color: var(--color-1)}
  32%   {color: var(--color-1)}
  33%   {color: var(--color-2)}
  65%   {color: var(--color-2)}
  66%   {color: var(--color-3)}
  99%   {color: var(--color-3)}
  100%  {color: var(--color-1)}
}

.search-box .search-bar {
    display: block;
  width: 50%;
  padding: 15px;
  
  color: #313131;
  font-size: 20px;
  appearance: none;
  border:none;
  outline: none;
  background: none;
  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.5);
  transition: 0.4s;
  border-radius: 16px;
}
</style>
