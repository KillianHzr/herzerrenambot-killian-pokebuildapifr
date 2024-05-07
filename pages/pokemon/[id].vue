<template>
  <div v-if="pokemon" class="max-w-lg mx-auto my-8 p-6 bg-white shadow-lg rounded-lg">
    <h1 class="text-3xl font-bold text-center mb-6">{{ pokemon.name }}</h1>
    <img :src="pokemon.image" :alt="pokemon.name" class="mx-auto mb-6 w-32 h-32 object-cover rounded-full border-4 border-yellow-300" />
    <div class="flex justify-center mb-6">
      <div v-for="type in pokemon.apiTypes" :key="type.name" class="mx-1">
        <img :src="type.image" :alt="type.name" class="w-10 h-10 rounded-full border border-gray-300" />
      </div>
    </div>
    <div class="text-center space-y-2">
      <p class="text-lg">HP: <span class="font-semibold">{{ pokemon.stats.HP }}</span></p>
      <p class="text-lg">Attack: <span class="font-semibold">{{ pokemon.stats.attack }}</span></p>
      <p class="text-lg">Defense: <span class="font-semibold">{{ pokemon.stats.defense }}</span></p>
      <p class="text-lg">Speed: <span class="font-semibold">{{ pokemon.stats.speed }}</span></p>
    </div>
    <button 
      @click="toggleTeam(pokemon)" 
      :class="['text-white font-semibold py-2 px-4 rounded transition', 
                isInTeam ? 'bg-red-700 hover:bg-red-500 border-red-700' : 'bg-blue-700 hover:bg-blue-500 border-blue-700']">
      {{ isInTeam ? '- TEAM' : '+ TEAM' }}
    </button>
  </div>
</template>

<script setup>
import { computed, ref } from 'vue'
const route = useRoute()
const id = route.params.id

const { data: pokemon } = await useFetch(`https://pokebuildapi.fr/api/v1/pokemon/${id}`)
const team = useState('team', () => [])

const isInTeam = ref(false)

watchEffect(() => {
    isInTeam.value = team.value.some(p => p.id === pokemon.value.id)
})

function toggleTeam(pokemon) {
  if (isInTeam.value) {
    team.value = team.value.filter(p => p.id !== pokemon.id)
  } else if (team.value.length < 6) {
    team.value.push(pokemon)
  } else {
    alert("Your team is already full!")
  }
}
</script>
