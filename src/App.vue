<template>
    <div>
      <h1>Countries</h1>
    </div>
</template>

<script>
export default {
  name: 'app',
  data(){
    return {
      countries: [],
      selectedCountry: null
    }
  },
  mounted(){
    fetch('https://restcountries.eu/rest/v2/all')
    .then(res => res.json())
    .then(countries => this.countries = countries)
  },
  components: {
    "countries-list": CountriesList
  }
}
</script>

<style>

</style>
