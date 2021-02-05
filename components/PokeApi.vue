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
    <div v-if="!$fetchState.pending && !$fetchState.error">
      <h3 class="title">{{ pokemon.name }}</h3>
      <div class="abilities">
        <p v-for="ability in pokemon.abilities">{{ ability.ability.name }}</p>
      </div>
      <img type="svg" :src="pokemon.sprites.other.dream_world.front_default" />
    </div>
  </div>
</template>
<script>
export default {
  data () {
    return {
      pokemonInput: '1',
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
img {
  width: 30%;
}
.abilities {
  color: #526488;
  display: flex;
  margin: 0 auto 0 auto;
  justify-content: space-around;
}
</style>
