<script setup>
import { onMounted,reactive,ref,computed } from 'vue';
import listPokemon from '../components/listPokemon.vue';
import CardPokemonSelected from '../components/CardPokemonSelected.vue';

let urlBase = ref("https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/");
let pokemons = reactive(ref());
let searchPokemonField = ref("");
let pokemonSelected = reactive(ref());
let loading = ref(false);

onMounted( ()=>{
    fetch("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
    .then( res => res.json())
    .then(res => {
        pokemons.value = res.results;
        console.log(pokemons);
    });
})

const searhPokemon = computed(()=>{
   if(pokemons.value && searchPokemonField.value){
       return pokemons.value.filter(pokemon=>
           pokemon.name.toLowerCase().includes(
            searchPokemonField.value.toLowerCase())
       )
   }
   return pokemons.value;
})

const selectPokemon = async (pokemon) =>{
  loading.value = true;
  await fetch(pokemon.url)
  .then(res => res.json())
  .then(res => pokemonSelected.value = res)
  .catch(err => alert(err))
  .finally(()=> loading.value = false)

  console.log(pokemonSelected.value);
}

</script>

<template>
  <main>
      <div class="container">

        <div class="row mt-4">

        <div class="col-sm-12 col-md-6" >
          <div class="card" >
            <div class="card=body row " >
            <CardPokemonSelected 
             :name="pokemonSelected?.name"
             :xp="pokemonSelected?.base_experience"
             :height="pokemonSelected?.height" 
             :img="pokemonSelected?.sprites.other.dream_world.front_default"
             :loading="loading"                     
            />
        </div>
        </div>
        </div>  
          
          <div class="col-sm-12 col-md-6 col mb-2" >
            <div class="card" >
              <div class="card=body row " >
                <div class="mb-3">
                  <span hidden class="form-label" for="searchPokemonField"></span>
                  <input v-model="searchPokemonField" type="text" 
                       class="form-control" placeholder="Pesquisar..." 
                       id="searchPokemonField"
                  >
                </div>


              <listPokemon 
                v-for="pokemon in searhPokemon"
                :key="pokemon.name"
                :name="pokemon.name"
                :urlBase = "urlBase + pokemon.url.split('/')[6] + '.svg'"
                @click="selectPokemon(pokemon)"
              />
            </div>
            </div>
          </div>
          
          
        </div>
      </div>

  </main>
</template>

<style scoped>
.card-list{
  max-height: 75vh;
  overflow-y: scroll;
  overflow-x: hidden;
}

@media (max-width: 768px) {
  .card-list{
    max-height: 48vh;
  }
}
</style>