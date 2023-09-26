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