<template>
  <div class="max-w-7xl mx-auto py-12 mb-32">
    <div class="w-100 flex justify-center mb-16">
      <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/98/International_Pok%C3%A9mon_logo.svg/2560px-International_Pok%C3%A9mon_logo.svg.png" width="300">
    </div>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
      <PokemonCard
        v-for="pokemon in pokemons"
        :key="pokemon.id"
        :pokemon="pokemon"
        :inTeam="team.includes(pokemon)"
        @toggle="toggleTeam"
      />
    </div>
  </div>
</template>

<script setup>
const { data: pokemons } = await useFetch('https://pokebuildapi.fr/api/v1/pokemon')
const team = useState('team', () => [])

function toggleTeam(pokemon) {
  if (team.value.includes(pokemon)) {
    team.value = team.value.filter(p => p.id !== pokemon.id)
  } else if (team.value.length < 6) {
    team.value.push(pokemon)
  } else {
    alert("Your team is already full!")
  }
}
</script>
