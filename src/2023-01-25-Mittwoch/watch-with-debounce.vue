<script setup lang="ts">
import { ref, watch } from 'vue';
import { CraftBeer } from '../interfaces';
const beerList = ref<CraftBeer[]>([])
const filter = ref('')

// Declare the debounce Timeout Variable 
// (we need it to reset the timeout)
let debounceTimeout: number | null = null

// use watch to update the timer when changes 
// happen to the rective variable filter.
watch(filter, async (newFilter) => {

  // if debounceTimeout is already set -> 
  // clear the timeout to stop its execution
  if (debounceTimeout != null) { clearTimeout(debounceTimeout) }

  // set a new Timeout with a callback which fetches data from the API
  debounceTimeout = setTimeout(async () => {
    const response = await fetch('https://fruityvice.com/api/fruit/all')
    beerList.value = await response.json()

    // set the debounceTimeout to null after the execution finishes
    debounceTimeout = null
  }, 500)
}, { immediate: true })
</script>

<template>
  <div class="bg-stone-800 text-white flex flex-col items-center min-h-screen min-w-max">
    <div class="flex flex-col w-fit">
      <div class="flex items-center space-x-4">
        <div class="text-3xl mb-4 h-8">Beers</div>
        <input class="bg-stone-900 p-2 rounded-lg h-8" type="text" placeholder="name" v-model="filter">
      </div>
      <template v-for="beer in beerList" :key="beer.id">
        <div class="bg-stone-900 mb-2 p-4 flex items-center space-x-4 rounded-lg">
          <img class="w-4" v-if="beer.image_url != null" :src="beer.image_url" :alt="`Image of ${beer.name}`">
          <div>
            <span>{{ beer.id }}</span>
            {{ beer.name }}
            <p class="text-xs max-w-md">{{ beer.brewers_tips }}</p>
          </div>
        </div>
      </template>
    </div>
  </div>
</template>
