# PokeApi
+ Análise e Desenvolvimento de Sistemas<br/>
+ Desenvolvimento. Aplicações Web<br/>
+ Arthur Cruz Modena <br/>
+ Ra:1945514<br/>
+ Completar uma Api de Pokemon<br/>


<h3>Bem vindo à API Pokemon</h3>

>status: Iniciando 

## Esta Api possui as seguintes funções conectadas ao: "https://pokeapi.co/api/v2/pokemon/?limit=151&offset=0";
+ Poderá pesquisar qualquer dos 151 pokemons pelo nome
+ Irá mostrar seu Xp e tamanho
+ Irá mostrar sua imagem quando selecionado ou apenas demonstrará com os outros

<p>No PokemonCard é criado o tipo de espaço em que os pokemons serão armazenados, sua "Card".
Fora algumas informações como seu Xp e Altura</p>
<script setup> 
const pokemon = defineProps(["Name","xp","height","img"])
</script>
<template>
    <div class="card">
            <img 
            :src="pokemon.img" class="card-img-top" 
            :alt="pokemon.name">
            <div class="card-body">
                <h5 class="card-title text-center">{{pokemon.name}}</h5>
                
                <hr> 
                <div class="row">
                    <section class="col">
                        <strong>XP:</strong>
                        <span>{{pokemon.xp}}</span>
                    </section>
                    <section class="col">
                        <strong>height:</strong>
                        <span>{{pokemon.height}}</span>
                    </section>
                </div>
            </div>
        </div>
</template>
<style>
</style>


## Em ListPokemons é utilizado para escolher de onde será tirado os nomes e outras informações dos Pokemons
<script setup>
const pokemon = defineProps(["name","baseUrlSvg"])

</script>

<template>
    <div class="col-4">
        <div class="card p-2 mb-3">
            <p class="text-center">{{ pokemon.name }}</p>
            <img
            :src="baseUrlSvg" class="card-img-top"
            alt="..."
            height="80"
                />
        </div>
    </div>
     

</template>

<style>
.container {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 10px;
    width: calc(100% - 20px);
    min-height: calc(100vh - 20px);
    
    font-family: 'acme', arial;
    font-size: 1rem;
}
</style>

## Por último HomeView, onde será estruturado as importações dos pokemons por meio das classes, coletando os valores e informações diretos do próprio PokeApi/v2 e <br> construindo as cartas que é onde são armazenados. 

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



