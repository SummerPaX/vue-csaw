<script setup lang="ts">
import { ref } from "vue";

const emojis = ["✌", "👊", "✋"];

const pointsPlayer = ref(0);
const pointsComputer = ref(0);

const playerAttack = ref("");
const computerAttack = ref("");

const vsColor = ref("");

function attack(emoji: string) {
	playerAttack.value = emoji;

	// generate random emoji for Computer
	const randomNumber = Math.floor(Math.random() * 3); // generates a random Number from 0 - 2
	computerAttack.value = emojis[randomNumber];

	// calculate Winner
	if (
		(playerAttack.value === "✌" && computerAttack.value === "✋") ||
		(playerAttack.value === "👊" && computerAttack.value === "✌") ||
		(playerAttack.value === "✋" && computerAttack.value === "👊")
	) {
		pointsPlayer.value++;
		vsColor.value = "bg-green-500";
	} else if (playerAttack.value === computerAttack.value) {
		vsColor.value = "bg-amber-500";
	} else {
		pointsComputer.value++;
		vsColor.value = "bg-red-500";
	}
}
</script>

<template>
	<div class="flex justify-between p-8">
		<div class="flex flex-col items-center gap-2">
			<h1 class="text-3xl">Player</h1>
			<p>Points: {{ pointsPlayer }}</p>
			<div>
				<button @click="attack('✌')" class="p-1 bg-stone-200 rounded">✌</button>
				<button @click="attack('👊')" class="p-1 bg-stone-200 rounded">👊</button>
				<button @click="attack('✋')" class="p-1 bg-stone-200 rounded">✋</button>
			</div>
		</div>
		<div class="flex justify-center items-center gap-2 text-3xl">
			<span> {{ playerAttack }}</span>
			<span :class="vsColor" class="p-1 rounded font-medium">VS</span>
			<span> {{ computerAttack }}</span>
		</div>
		<div class="flex flex-col items-center gap-2">
			<h1 class="text-3xl">Computer</h1>
			<p>Points: {{ pointsComputer }}</p>
		</div>
	</div>
</template>
