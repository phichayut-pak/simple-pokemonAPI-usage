<template>
  <div id="app">
    <navbar></navbar>
    <pokemon-api pokemon="pikachu"></pokemon-api>
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue'
import PokemonApi from './components/PokemonApi.vue'

export default {
  name: 'App',
  components: {
    PokemonApi, Navbar
  }
}
</script>

<style>

</style>
