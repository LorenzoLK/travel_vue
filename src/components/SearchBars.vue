<template>
    <div class="search-box">
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

    <div class='weather-info' v-if="typeof weather.main != 'undefined'">
            <div class="location-hub">
            <div class="">{{ weather.name }}</div>
            <div class="">{{ Math.round(weather.main.temp) }}°F</div>
            </div>
    </div>

    <div>
        <div class="'flight-info" v-if="typeof travel.main != 'undefined'">
        <div class="location-hub">
          <div class="">{{ travel.name }}</div>
          <div class="">{{ Math.round(travel.main.currency) }}°F</div>
        </div>
      </div>
    </div>
</template>

<script>
    export default {
        name:'SearchBars',
 
        data() {
            return {
                query_depart_loc: '',
                query_arrive_loc: '',
                query_depart_date: '',
                query_arrive_date: '',
                travel_api_key: 'd054f71cacmsh045112f43332108p1229fejsn8281182815f5',
                travel_url_base: 'https://skyscanner-skyscanner-flight-search-v1.p.rapidapi.com/apiservices',
                travel: {},
                weather_api_key: '938b78026546140d37edf372f2b40f89',
                weather_url_base: 'https://api.openweathermap.org/data/2.5/',
                weather: {}
            }
        },
    methods: {
    async fetchInfo(e) {
        if (e.key == 'Enter'){
            let response = await fetch(`${this.weather_url_base}weather?q=${this.query_depart}&units=imperial&APPID=${this.weather_api_key}`);
            let json= await response.json();
            this.weather = await json;

            /*travel.depart = this.query_depart_loc;
            travel.arrive = this.query_arrive_loc;
            travel.depart_date = this.query_depart_date;
            travel.arrive_date = this.query_arrive_date;
            
            let travelRes = await fetch(`${this.travel_url_base}travel?q=${this.query_depart_loc}/
            ${this.travel.depart}/
            ${this.travel.arrive}/
            ${this.travel.depart_date}/
            ${this.travel.arrive_date}`);
            let travelJSON = await travelRes.json();
            this.travel = await travelJSON;*/
        }
    }
  }
    }
</script>

<style>
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
        margin: 10px 0px;
    }
</style>