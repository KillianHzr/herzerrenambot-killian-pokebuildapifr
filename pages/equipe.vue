<template>
  <div class="max-w-7xl mx-auto p-8">
    <h1 class="text-3xl font-bold mb-8 text-center">My Pokémon Team</h1>

    <div v-if="uniqueTypes.length > 0" class="flex flex-wrap justify-center gap-4">
      <div
        v-for="type in uniqueTypes"
        :key="type.name"
        class="flex items-center space-x-2 bg-gray-100 px-4 py-2 rounded-full"
      >
        <img :src="type.image" :alt="type.name" class="w-6 h-6 object-cover rounded-full" />
        <span class="font-medium text-gray-800">{{ type.name }}</span>
      </div>
    </div>
    <div v-else class="text-center text-gray-500">
      <p>No types available</p>
    </div>

    <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-6 gap-6 mt-8">
      <PokemonCard
        v-for="pokemon in team"
        :key="pokemon.id"
        :pokemon="pokemon"
        :inTeam="true"
        @toggle="toggleTeam"
      />
      <div
        v-for="n in 6 - team.length"
        :key="`empty-${n}`"
        class="border-2 border-dashed border-gray-300 rounded-lg h-40 flex items-center justify-center text-gray-500"
      >
        <p>Empty Slot</p>
      </div>
    </div>
  </div>
</template>

<script setup>
const team = useState('team', () => [])

function toggleTeam(pokemon) {
  team.value = team.value.filter(p => p.id !== pokemon.id)
}

const uniqueTypes = computed(() => {
  const typesMap = new Map()
  team.value.forEach(pokemon => {
    pokemon.apiTypes.forEach(type => {
      if (!typesMap.has(type.name)) {
        typesMap.set(type.name, type)
      }
    })
  })
  return Array.from(typesMap.values())
})
</script>
