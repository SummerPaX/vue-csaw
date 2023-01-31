<script setup lang="ts">
// const props = defineProps(["title", "body"]);

const props = defineProps<{
	title: string;
	body?: string;
}>();

const emit = defineEmits(["favouriteBlog"]);

// const emit = defineEmits<{
// 	(e: "favouriteBlog", favorite: boolean): void;
// }>();
</script>

<template>
	<div>
		<h1 class="text-2xl">{{ title }}</h1>
		<p>{{ body }}</p>
		<button class="bg-stone-200 p-2 rounded" @click="emit('favouriteBlog')">💗</button>
	</div>
</template>
