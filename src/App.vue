<template>
    <div>
      <h1>Countries</h1>

        <div> <!-- Drop down: select from a lost of all countries  -->
          <label for="country-select">Select a country:</label>
          <select id='country-select' v-model="selectedCountry">
            <option disabled value="">Select a country</option>
            <option v-for="(country, index) in countries" :key="index" :value="country">{{country.name}}</option>
          </select>
          <country-detail :country='selectedCountry'></country-detail>
        </div>

        <div><!-- Search box: Find countries by name  -->
          <label for="country-search">Search by name: </label>
          <input type="text" v-model="search" placeholder="Search country..." />
        </div>

        <div class="main-container" >
          <countries-list :countries="countries" v-bind="countries"></countries-list>
          <country-detail :country='selectedCountry'></country-detail>
        </div>
    </div>
</template>

<script>
import {eventBus} from './main.js';
import CountriesList from './components/CountriesList.vue';
import CountryDetail from './components/CountryDetail.vue';

export default {
  name: 'app',
  data(){
    return {
      countries: [],
      selectedCountry: null,
      search: ""
    }
  },
  mounted(){
    fetch('https://restcountries.eu/rest/v2/all')
    .then(res => res.json())
    .then(countries => this.countries = countries)

    eventBus.$on('country-selected', (country) => {
      this.selectedCountry = country
    })
  },
  components: {
    "countries-list": CountriesList,
    "country-detail": CountryDetail
  },
  computed: {
    filteredList() {
      return this.countries.filter(country => {
        return country.name.toLowerCase().includes(this.search.toLowerCase())
      })
    }
  }
}
</script>

<style>
  .main-container {
    display: flex;
    justify-content: space-between;
  }
</style>
