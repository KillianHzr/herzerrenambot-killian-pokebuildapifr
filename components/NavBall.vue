<template>
  <div class="fixed bottom-3 z-10 w-full flex justify-center" style="pointer-events: none">
    <div class="flex flex-col items-center justify-between rounded-full overflow-hidden border-4 border-black">
      <div class="flex items-center justify-center w-full h-1/2 bg-red-600 border-b-black border-b-2">
        <NuxtLink
          v-for="{ href, name } in topMenuItems"
          :to="href"
          class="flex-1 text-center py-3 px-5 text-white hover:bg-red-700" style="pointer-events: initial">
          {{ name }}
        </NuxtLink>
      </div>
      <div class="absolute w-6 h-6 bg-white border-4 border-black rounded-full flex items-center justify-center" style="top: 50%; left: 50%; transform: translate(-50%, -50%);">
        <div class="w-2 h-2 border-black border-2 bg-white rounded-full"></div>
      </div>
      <div class="flex items-center justify-center w-full h-1/2 bg-white border-t-black border-t-2">
        <NuxtLink
          v-for="{ href, name } in bottomMenuItems"
          :to="href"
          class="flex-1 text-center py-3 text-black hover:bg-gray-300" style="pointer-events: initial">
          {{ name }}
        </NuxtLink>
      </div>
    </div>
  </div>
</template>


<script setup>
const topMenuItems = [
  { name: 'Pokedex', href: '/' },
]
const bottomMenuItems = [
  { name: 'Team', href: '/equipe' },
]
</script>