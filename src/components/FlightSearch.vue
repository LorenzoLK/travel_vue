<template>
    <div>
        <!-- <div class="'flight-info" v-if="typeof travel.main != 'undefined'">
        <div class="location-hub">
          <div class="">{{ travel.name }}</div>
          <div class="">{{ Math.round(travel.main.currency) }}°F</div>
        </div>
      </div> -->
    </div>
</template>

<script>
export default {
    name: 'FlightSearch',
    data() {
        return {
            travel_api_key: 'd054f71cacmsh045112f43332108p1229fejsn8281182815f5',
            travel_url_base: 'https://partners.api.skyscanner.net/apiservices/browsequotes/v1.0/US/USD/en-US/',
            travel: {}
        }
    }
}
</script>

<style>

</style>