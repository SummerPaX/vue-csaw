<script setup lang="ts">
import { StarWarsAPICharacter } from "../interfaces";

defineProps<{
	character: StarWarsAPICharacter;
}>();

defineEmits<{
	(e: "delete", url: string): void;
}>();
</script>

<template>
	<div class="bg-stone-800 text-white flex flex-col items-center w-full">
		<div class="flex flex-col w-full">
			<div class="bg-stone-900 p-4 flex items-center space-x-4 rounded-lg">
				<div>
					<span>{{ character.name }}</span>
					<p class="text-xs max-w-md">Größe: {{ character.height }}</p>
					<p class="text-xs max-w-md">Masse: {{ character.mass }}</p>
					<p class="text-xs max-w-md">Augenfarbe: {{ character.eye_color }}</p>
					<p class="text-xs max-w-md">Haarfarbe: {{ character.hair_color }}</p>
					<button class="bg-stone-600 p-2" @click="$emit('delete', character.url)">Delete</button>
				</div>
			</div>
		</div>
	</div>
</template>

<style></style>
