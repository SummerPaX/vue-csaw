<script setup lang="ts">
import { ref } from 'vue';

const km = ref(0)
const celsius = ref(0)
</script>

<template>
  <div class="bg-stone-800 text-white flex flex-col justify-center items-center min-h-screen">
    <div class="flex flex-col w-fit">
      <div class="flex flex-wrap  justify-between items-center mb-4">
        <input class="bg-stone-900 p-2 rounded-lg w-16" type="number" v-model="km">
        <label for="km" class="px-1">km</label>
        <span class="mr-auto">»</span>
        <div class="px-1">Miles: {{ (km / 1.609).toFixed(2) }}</div>
      </div>
      <div class="flex flex-wrap justify-between items-center ">
        <input class="bg-stone-900 p-2 rounded-lg w-16" type="number" v-model="celsius">
        <label for="km" class="px-1">°C</label>
        <span class="mr-auto">»</span>
        <div class="px-1">Fahrenheit: {{ ((celsius * 9 / 5) + 32).toFixed(2) }}</div>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>
