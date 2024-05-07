<template>
  <div class="fixed bottom-3 z-10 w-full flex justify-center" style="pointer-events: none">
    <div class="flex flex-col items-center justify-between rounded-full overflow-hidden border-4 border-black">
      <div class="flex items-center justify-center w-full h-1/2 border-b-black border-b-2 background-active-option">
        <NuxtLink
          v-for="{ href, name } in topMenuItems"
          :to="href"
          class="flex-1 text-center py-3 px-5"
          style="pointer-events: initial">
          {{ name }}
        </NuxtLink>
      </div>
      <div
        :class="circleClass"
        class="absolute w-6 h-6 border-4 border-black rounded-full flex items-center justify-center"
        style="top: 50%; left: 50%; transform: translate(-50%, -50%);">
        <div :class="innerCircleClass" class="w-2 h-2 border-2 rounded-full"></div>
      </div>
      <div class="flex items-center justify-center w-full h-1/2 border-t-black border-t-2 background-active-option">
        <NuxtLink
          v-for="{ href, name } in bottomMenuItems"
          :to="href"
          class="flex-1 text-center py-3"
          style="pointer-events: initial">
          {{ name }}
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'
import { useRoute } from 'vue-router'

const topMenuItems = [
  { name: 'Pokedex', href: '/' },
]
const bottomMenuItems = [
  { name: 'Team', href: '/equipe' },
]

const route = useRoute()

const anyLinkActive = computed(() => {
  return topMenuItems.concat(bottomMenuItems).some(item => route.path === item.href)
})

const circleClass = computed(() => {
  return anyLinkActive.value ? 'bg-white' : 'bg-red-500'
})

const innerCircleClass = computed(() => {
  return anyLinkActive.value ? 'bg-white border-black' : 'bg-red-500 border-red-700'
})
</script>

<style scoped>
.background-active-option a {
  background: white;
}

.background-active-option a:hover {
  background: rgb(222, 222, 222);
}

.router-link-active, .router-link-exact-active {
  background: #e73124 !important;
  color: white !important;
}

.router-link-active:hover, .router-link-exact-active:hover {
  background: #b7241a !important;
}
</style>
