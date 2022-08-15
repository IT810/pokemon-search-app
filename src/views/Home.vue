<template>
    <div class="w-full flex justify-center">
        <input type="text" placeholder="Enter pokemon here" class="mt-10 p-2 border-blue-500 border-2 w-80 rounded-md" v-model="text" />
    </div>
    <div class="my-10 p-4 flex flex-wrap justify-center">
        <div v-if="filteredPokemons.length <= 0">No data</div>
        <div class="m-2 text-2x text-blue-500 p-3 bg-green-300 rounded-md hover:bg-sky-700" v-for="(pokemon, idx) in filteredPokemons" :key="idx">
            <router-link :to="`/about/${urlIdLookUp[pokemon.name]}`">{{ pokemon.name }}</router-link>
        </div>
    </div>
</template>

<script>
import { reactive, toRefs, computed } from 'vue';

export default {
    name: 'HomeComponent',
    setup() {
        const state = reactive({
            pokemons: [],
            urlIdLookUp: {},
            text: "",
            filteredPokemons: computed(() => updatePokemon())
        });

        function updatePokemon() {
            if (state.text === "") {
                return [];
            }
            var s = state.pokemons.filter(x => x.name.startsWith(state.text));
            console.log(s);
            return s;
        }

        fetch("https://pokeapi.co/api/v2/pokemon?offset=0&limit=900")
            .then((res) => res.json())
            .then((data) => {
                console.log(data.results);
                state.pokemons = data.results;
                state.urlIdLookUp = data.results.reduce((acc, cur, idx) => acc = { ...acc, [cur.name]: idx + 1 }, {});
            });

        return {
            ...toRefs(state),
        }
    },
    created() {
    }
}
</script>

<style>
</style>