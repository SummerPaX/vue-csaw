<script setup lang="ts">
import { computed, ref } from 'vue';

const position = ref({
  top: 0,
  left: 0
})

const transform = computed(() => {
  return { top: position.value.top + 'px', left: position.value.left + 'px' }
})

function up() {
  position.value.top--
}

function left(amount: number, event: KeyboardEvent) {
  if ((<HTMLDivElement>event.target).offsetLeft > 0) {
    position.value.left--
  }
}

function submit(event: Event) {
  alert('Hi')
  // Code....
}


</script>

<template>
  <div @keydown.down="position.top++" @keydown.up="up" @keydown.left="(event) => left(1, event)"
    @keydown.right="position.left++" tabindex="0" class="absolute w-24 h-24 bg-green-600" :style="transform">
    <div class=" w-12 h-12 bg-amber-400"></div>
  </div>
  <form class="absolute top-[100px] m-auto" action="submit" @submit.prevent="submit">
    <button>Press me</button>
  </form>
</template>

<style scoped>

</style>
