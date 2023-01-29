<script setup lang="ts">
import { onMounted, ref } from "vue";
import StarWarsCharacterCard from "./StarWarsCharacterCard.vue";
import { StarWarsAPICharacter, StarWarsAPICharacterList } from "../interfaces";

const characters = ref<StarWarsAPICharacter[]>();

onMounted(async () => {
	const response = await fetch("https://swapi.dev/api/people/");
	let data: StarWarsAPICharacterList = await response.json();

	characters.value = data.results;
});

function deleteCharacter(url: string) {
	characters.value = characters.value?.filter((character) => character.url !== url);
}
</script>

<template>
	<div class="grid grid-cols-3 bg-stone-800 gap-2">
		<StarWarsCharacterCard @delete="deleteCharacter" v-for="character in characters" :key="character.url" :character="character" />
	</div>
</template>

<style></style>
