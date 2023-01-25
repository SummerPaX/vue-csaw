<script setup lang="ts">
import { computed, onMounted, ref, watch, watchEffect } from 'vue';
import { CraftBeer } from './interfaces';
const beerList = ref<CraftBeer[]>([])

let debounceTimeout: number | null = null
const filter = ref('')
const food = ref('')

watch([filter, food], async ([newFilter, newFood]) => {
  if (debounceTimeout != null) { clearTimeout(debounceTimeout) }

  debounceTimeout = setTimeout(async () => {
    let query = ''
    if (newFilter != '' || newFood != null) {
      let param = new URLSearchParams()
      if (newFilter) {
        param.append('beer_name', newFilter)
      }
      if (newFood) {
        param.append('food', newFood)
      }

      query = '?' + param.toString()
    }

    const response = await fetch('https://api.punkapi.com/v2/beers/' + query)
    const json: CraftBeer[] = await response.json()

    beerList.value = json
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
        <input class="bg-stone-900 p-2 rounded-lg h-8" type="text" placeholder="food" v-model="food">
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

<style scoped>

</style>
