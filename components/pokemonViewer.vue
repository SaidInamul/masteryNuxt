<script setup>
import { ref, computed } from "vue";
import { useRoute } from "vue-router";

const pokemonList = ref([]);
const route = useRoute();

const pokemonTypes = computed(() => {
    const types = pokemonList.value.flatMap((pokemon) =>
        pokemon.types.map((type) => type.type.name),
    );

    return [...new Set(types)];
});

const filterElement = computed(() => {
    if (route.query.element === undefined) {
        return pokemonList.value;
    }
    const queryType = route.query.element.toLowerCase();
    return pokemonList.value.filter(
        (pokemon) => pokemon.types.some((type) => type.type.name === queryType), // Check if type matches
    );
});

onMounted(() => {
    try {
        // Fetch the list of Pokémon (names + URLs)
        fetch("https://pokeapi.co/api/v2/pokemon?limit=100")
            .then((response) => response.json())
            .then((json) => {
                const pokemonUrl = json.results;

                // Fetch the details of the pokemons
                // use all() to form an array of promises and wait to return all resolves (success promises)
                // If any single promises return reject, the Promises.all() will return reject
                Promise.all(
                    pokemonUrl.map(async (pokemon) => {
                        const response = await fetch(pokemon.url);
                        const json = await response.json();
                        return json;
                    }),
                )
                    .then((json) => {
                        pokemonList.value = json;
                    })
                    .catch((error) => {
                        console.log("Error : " + error);
                    });
            });
    } catch (error) {
        console.error("Error fetching Pokémon data:", error);
    }
});
</script>

<template>
    <BaseViewer class="space-y-5" title="Pokemon API">
        <template v-slot:heading>
            <p>{{ pokemonTypes.length }} elements of pokemons</p>
            <p>{{ filterElement.length }} pokemons listed</p></template
        >
        <template v-slot:content>
            <div class="flex items-center space-x-2">
                <div><p>Elements:</p></div>
                <div class="flex flex-wrap items-center gap-3">
                    <NuxtLink
                        v-for="(type, index) in pokemonTypes"
                        :key="index"
                        :to="`/display/pokemon?element=${type}`"
                    >
                        <UBadge color="primary" variant="soft" :label="type"
                    /></NuxtLink>
                </div>
            </div>
            <ul
                class="grid gap-3"
                :class="
                    route.name === 'display-pokemon'
                        ? 'grid-cols-4'
                        : 'grid-cols-2'
                "
            >
                <li
                    v-for="pokemon in filterElement"
                    :key="`pokemon-id-${pokemon.id}`"
                    class="p-3 bg-green-100 rounded-lg flex items-center gap-3 hover:bg-green-200"
                >
                    <div>
                        <img
                            :src="pokemon.sprites.front_default"
                            alt="pokemon sprites"
                        />
                    </div>
                    <div>
                        <p class="font-medium text-lg capitalize">
                            {{ pokemon.name }}
                        </p>
                        <div class="space-x-2">
                            <UBadge
                                v-for="(types, index) in pokemon.types"
                                :key="index"
                                :label="types.type.name"
                            >
                            </UBadge>
                        </div>
                    </div>
                </li>
            </ul>
        </template>
    </BaseViewer>
</template>
