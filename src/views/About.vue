<template>
    <div class="about">
        <div v-if="pokemon" class="w-4/5 m-auto bg-purple-100 mt-4 shadow-2xl flex justify-center flex-col items-center">
            <h3 class="text-2xl text-green-900 uppercase my-4">{{pokemon.name}}</h3>
            <div class="flex justify-center w-full">
                <img :src="pokemon.sprites.front_shiny" class="w-1/5" />
                <img :src="pokemon.sprites.back_shiny" class="w-1/5" />
            </div>
            <h3 class="text-yellow-400">Types</h3>
            <div v-for="(type, idx) in pokemon.types" :key="idx">
                <h5 class="text-blue-900">{{type.type.name}}</h5>
            </div>
        </div>
    </div>
</template>

<script>
import { reactive, toRefs } from 'vue';
import { useRoute } from 'vue-router';
export default {
    name: 'AboutComponent',
    setup() {
        const route = useRoute();
        const state = reactive({
            pokemon: null,
        });

        fetch(`https://pokeapi.co/api/v2/pokemon/${route.params.slug}/`)
            .then((res) => res.json())
            .then((data) => {
                console.log(data);
                state.pokemon = data;
            });

        return{
            ...toRefs(state),
        }
    }
}
</script>

<style>
</style>