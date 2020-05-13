<template lang="html">
  <div v-if="country">
      <h3> {{ country.name }} </h3>
      <p>Capital: {{country.capital}} </p>
      <p>Population: {{country.population}} </p>
      <h4>Languages: </h4>
      <p v-for="language in country.languages">{{language.name}}</p>
      <img class="lrg-flag" :src="country.flag" />
  </div>
</template>

<script>
export default {
    name: 'country-detail',
    props: ['country']
}
</script>

<style>

</style>