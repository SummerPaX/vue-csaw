<script setup lang="ts">
const props = defineProps<{
	history: string[];
}>();

const emit = defineEmits<{
	(e: "restoreHistory", item: string): void;
}>();
</script>

<template>
	<div
		class="flex flex-col justify-items-center min-w-[6rem] py-4 rounded-sm border-2 border-stone-900"
	>
		<span
			v-for="item in history"
			:key="item"
			@click="emit('restoreHistory', item)"
			class="hover:bg-neutral-600 h-6 px-2 cursor-pointer w-full"
			>{{ item }}</span
		>
	</div>
</template>
