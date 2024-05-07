<template>
  <div class="max-w-7xl mx-auto py-12 mb-32">
    <div class="w-100 flex justify-center mb-16">
      <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/98/International_Pok%C3%A9mon_logo.svg/2560px-International_Pok%C3%A9mon_logo.svg.png" width="300">
    </div>

    <div class="flex justify-center mb-8">
      <input
        v-model="searchQuery"
        type="text"
        placeholder="Search Pokémon..."
        class="p-2 border rounded-lg w-full md:w-1/2"
      />
    </div>

    <div class="flex flex-wrap justify-center gap-4 mb-8">
      <div
        v-for="type in types"
        :key="type.name"
        class="flex items-center space-x-2 bg-gray-100 px-4 py-2 rounded-full cursor-pointer transition duration-200"
        :class="{'bg-blue-500 text-white': selectedTypes.includes(type.name)}"
        @click="toggleFilter(type)"
      >
        <img :src="type.image" :alt="type.name" class="w-6 h-6 object-cover rounded-full" />
        <span class="font-medium">{{ type.name }}</span>
      </div>
    </div>

    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
      <PokemonCard
        v-for="pokemon in filteredPokemons"
        :key="pokemon.id"
        :pokemon="pokemon"
        :inTeam="team.some(p => p.id === pokemon.id)"
        @toggle="toggleTeam"
      />
    </div>
  </div>
</template>

<script setup>
const { data: pokemons } = await useFetch('https://pokebuildapi.fr/api/v1/pokemon')
const { data: types } = await useFetch('https://pokebuildapi.fr/api/v1/types')

const team = useState('team', () => [])
const selectedTypes = ref([])
const searchQuery = ref('')

function toggleTeam(pokemon) {
  if (team.value.includes(pokemon)) {
    team.value = team.value.filter(p => p.id !== pokemon.id)
  } else if (team.value.length < 6) {
    team.value.push(pokemon)
  } else {
    alert("Your team is already full!")
  }
}

function toggleFilter(type) {
  if (selectedTypes.value.includes(type.name)) {
    selectedTypes.value = selectedTypes.value.filter(t => t !== type.name)
  } else {
    selectedTypes.value.push(type.name)
  }
}

const filteredPokemons = computed(() => {
  return pokemons.value.filter(pokemon => {
    const matchesType = selectedTypes.value.length === 0 || pokemon.apiTypes.some(type => selectedTypes.value.includes(type.name))
    const matchesSearch = pokemon.name.toLowerCase().includes(searchQuery.value.toLowerCase())
    return matchesType && matchesSearch
  })
})
</script>
