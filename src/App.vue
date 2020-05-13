<template>
    <div>
      <header>
        <h1>Countries</h1>

        <div class="search-container" id="search-for-country"><!-- Search box: Find countries by name  -->
          <label for="country-search">&#128269; </label>
          <input type="text" v-model="search" placeholder="Find a country..." />
        </div>
      </header>

      <section>
          <div class="main-container" id="select-country"> <!-- Drop down: select from a lost of all countries  -->
            <label for="country-select">Select a country:</label>
            <select id='country-select' v-model="selectedCountry">
              <option disabled value="">Select a country</option>
              <option v-for="(country, index) in countries" :key="index" :value="country">{{country.name}}</option>
            </select>
            <country-detail :country='selectedCountry'></country-detail>
          </div>
        </section>

        <div>  
          <countries-list :countries="filteredList" v-bind="countries"></countries-list>
        </div>

        <!-- <div class="main-container" >  Original list of countries
          <countries-list :countries="countries" v-bind="countries"></countries-list>
          <country-detail :country='selectedCountry'></country-detail>
        </div> -->
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

  body {
    font-family: Haettenschweiler, 'Arial Narrow Bold', sans-serif;
    
  }

  h1 {
    font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
    text-align: center;
  }

  header {
    background-color: palegreen;
    padding: 15px;
    position: relative;
    bottom: 10px;
  }

  .search-container {
    position: relative;
    bottom: 10px;
    float: right;
    font-size: 0.8em;
    color: rgb(85, 83, 83);
  }
</style>
