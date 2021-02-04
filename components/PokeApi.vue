<template>
  <div>
    <b-input-group class="mt-3">
      <b-form-input v-model="pokemonInput" placeholder="Pokemon"/>
      <b-input-group-append>
        <b-button @click="$fetch()" variant="outline-success">Encontrar Pokemon</b-button>
      </b-input-group-append>
    </b-input-group>
    <p v-if="$fetchState.pending">procurando pokemon...</p>
    <p v-if="$fetchState.error">pokemon não encontrado</p>
    <div v-if="!$fetchState.pending">
      <h3 class="title">{{ pokemon.name }}</h3>
      <p class="abilities" v-for="ability in pokemon.abilities">{{ ability.ability.name }}</p>
    </div>
  </div>
</template>
<script>
export default {
  data () {
    return {
      pokemonInput: '',
      pokemon: {}
    }
  },
  async fetch() {
    this.pokemon = await fetch(
      `https://pokeapi.co/api/v2/pokemon/${this.pokemonInput}`
    ).then(res => res.json())
  },
  fetchDelay: 900
}
</script>
<style>

@keyframes appear {
  0% {
    opacity: 0;
  }
}
.abilities {
  color: #526488;
}
</style>
