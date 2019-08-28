<template lang="html">
  <div class="">
    <h1>Countries of the World!!!</h1>
    <div class="main-container">
      <country-list :countries='countries'></country-list>
      <country-detail v-if="selectedCountry" :country="selectedCountry"></country-detail>
    </div>
  </div>
</template>

<script>
import CountryList from './components/CountryList.vue';
import CountryDetail from './components/CountryDetail.vue';
import {eventBus} from './main.js';

export default {
  name: 'app',
  data(){
    return {
      countries: [],
      selectedCountry: null
    };
  },
  mounted(){
    fetch('https://restcountries.eu/rest/v2/all')
    .then(res => res.json())
    .then(countries => this.countries = countries)

    eventBus.$on("country-selected", (country) => {
      this.selectedCountry = country;
    })
  },

  components: {
    "country-list": CountryList,
    "country-detail": CountryDetail
  }
}
</script>

<style lang="css" scoped>
.main-container {
  display: flex;
  justify-content: space-around;
}
</style>
