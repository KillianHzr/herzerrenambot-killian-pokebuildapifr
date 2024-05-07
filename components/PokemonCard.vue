<template>
  <div class="border rounded-lg shadow-lg p-6 text-center transition duration-300 transform hover:scale-105">
    <h2 class="text-xl font-semibold mb-4">{{ pokemon.name }}</h2>
    <img :src="pokemon.image" :alt="pokemon.name" class="mx-auto mb-6 w-24 h-24 object-cover" />
    <div class="flex flex-col gap-4">
      <nuxt-link 
        :to="'/pokemon/' + pokemon.id" 
        class="bg-transparent text-center hover:bg-yellow-500 text-blue-700 font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded transition">
        Afficher
      </nuxt-link>
      <button 
        @click="$emit('toggle', pokemon)" 
        :class="['text-white font-semibold py-2 px-4 rounded transition', 
                 inTeam ? 'bg-red-700 hover:bg-red-500' : 'bg-blue-700 hover:bg-blue-500']">
        {{ inTeam ? '- TEAM' : '+ TEAM' }}
      </button>
    </div>
  </div>
</template>

<script setup>
defineProps({
  pokemon: {
    type: Object,
    required: true
  },
  inTeam: {
    type: Boolean,
    required: true
  }
})
</script>
