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