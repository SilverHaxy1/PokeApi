<script setup>
import { onMounted, reactive, ref, computed } from 'vue';
import ListPokemons from '../components/listPokemons.vue';
import PokemonCard from '../components/PokemonCard.vue';


let baseUrlSvg = ref("https://raw.githubusercontent.com/PokeApi/sprites/master/sprites/pokemon/other/dream-world/")
let pokemons = reactive(ref());
let searchPokemonField = ref("")
let pokemonSelected = reactive(ref());

onMounted(() => {
  fetch("https://pokeapi.co/api/v2/pokemon/?limit=151&offset=0")
  .then(response => response.json())
  .then(response => {
    pokemons.value = response.results;
    console.log(response);
  })
})

const pokemonsFiltered = computed(()=>{
  if(pokemons.value && searchPokemonField.value){
    return pokemons.value.filter(pokemon=>
      pokemon.name.toLowerCase().includes(searchPokemonField.value.toLowerCase())
    )
  }
  return pokemons.value;
})

const selectPokemon = async (pokemon)=>{
  await fetch(pokemon.url)
  .then(res => res.json())
  .then(res => pokemonSelected.value = res);
  console.log(pokemonSelected.value);
}

</script>

<template>
  <main>
    <div class="container">
      <div class="row mt-4">
        <div class="col-sm-12 col-md-4">
          <PokemonCard 
          :name="pokemonSelected?.name"
          :xp="pokemonSelected?.base_experience"
          :height="pokemonSelected?.height"
          :img="pokemonSelected?.sprites.other.dream_world.front_default"
          />
        </div>
      <div class="col-sm-12 col-md-25">
        <div class="card">
          <div class="card-body row"> 
          <div class="mb-3">
            <label hidden for="searchPokemonField" class="form-label">Pesquisar</label>
            <input v-model="searchPokemonField" type="text" class="form-control" id="searchPokemonField" placeholder="Pesquisa">
            </div>
          <ListPokemons
          v-for="pokemon in pokemonsFiltered"
          :key="pokemon.name"
          :name="pokemon.name"
          :baseUrlSvg="baseUrlSvg + pokemon.url.split('/')[6] + '.svg'"
          @click="selectPokemon(pokemon)"/>
          </div>
        </div>
      </div>
    </div>
  </div>
  </main>
</template>

<style>
footer{
  position: fixed;
  bottom: 0;
  width: 15%;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 30px;
}

</style>
