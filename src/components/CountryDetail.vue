<template lang="html">
  <div v-if="country" class="info-box">
      <h3> {{ country.name }} </h3>
      <p>Capital: {{country.capital}} </p>
      <p>Population: {{country.population}} </p>
      <h4>Languages: </h4>
      <p v-for="language in country.languages">{{language.name}}</p>
      <img class="flag" :src="country.flag" />
  </div>
</template>

<script>
export default {
    name: 'country-detail',
    props: ['country']
}
</script>

<style>

.flag {
  max-width: 200px;
}

.info-box {
  background-color: silver;
  border: 1px solid grey;
  padding: 15px;
}

</style>