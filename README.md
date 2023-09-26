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




