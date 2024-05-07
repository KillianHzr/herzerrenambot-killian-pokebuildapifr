<template>
  <div>
    <h1 class="text-2xl font-bold mb-4">My Pokémon Team</h1>
    <div v-if="team.length > 0" class="pokemon-grid">
      <PokemonCard
        v-for="pokemon in team"
        :key="pokemon.id"
        :pokemon="pokemon"
        :inTeam="true"
        @toggle="toggleTeam"
      />
    </div>
    <div v-else class="text-gray-500">
      <p>No Pokémon in the team.</p>
    </div>
  </div>
</template>

<script setup>

const team = useState('team', () => [])

function toggleTeam(pokemon) {
  team.value = team.value.filter(p => p.id !== pokemon.id)
}
</script>

<style>
.pokemon-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}
</style>
