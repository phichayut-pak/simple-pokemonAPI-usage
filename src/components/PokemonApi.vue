<template>
  <div class="flex justify-center items-center py-16 mt-32">
    <div class="flex flex-col justify-start items-center max-w-2xl p-6 rounded-lg border-2 bg-gray-300 shadow-lg">
        <img :src="pokemon.pokemonURL" v-if="pokemon.pokemonURL.length != 0" class="h-96 w-96" alt="pokemon-picture">
      <div class="space-x-2">
        <input type="text" placeholder="Type your pokemon!" class="px-3 py-2 rounded-xl" @keyup.enter="onSubmit" v-model="findPokemon">
        <button @click="onSubmit" class="bg-green-400 p-2 rounded-xl">Submit</button>
      </div>
      <div>
        <p class="font-['Poppins'] text-sm text-red-500" v-if="error">*Invalid Name</p>      
      </div>
    </div>
    
    
  </div>

</template>

<script>
import axios from 'axios'
import Swal from 'sweetalert2'

export default {
  data() {
    return {
      pokemon: {
        pokemonName: "Type your pokemon!",
        pokemonURL: ""
      },
      findPokemon: "",
      error: false

    }
  },
  
  methods: {
    async fetchAPI(name){
      const url = `https://pokeapi.co/api/v2/pokemon/${name}?limit=1&offset=1`;
      try{
        await axios.get(url)
          .then(res => {
            this.pokemon.pokemonName = res.data.forms[0].name;
            this.pokemon.pokemonURL = res.data.sprites.front_default;
            this.findPokemon = ""
          })
      }catch(err) {
        if(err == "Error: Request failed with status code 404") {
          Swal.fire({
            icon: 'error',
            title: 'Invalid Name',
            text: 'Are you sure that it is a pokemon?',
          })
        }
      }
    },

    async onSubmit() {
      const name = this.findPokemon
      this.findPokemon = ""
      this.error = false
      this.fetchAPI(name)
    }
    
  },
  
}
</script>

<style>

</style>