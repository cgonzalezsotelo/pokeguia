<template>
  <div id="app" class="container">
    <div class="row">
      <div class="col text-center p-5">
        <img src="./assets/Pokemon-Logo.png" alt="logo pokemon" class="logo" />
        <h1 class="p-5 titulo">PokeGuía</h1>
        <label>Nombre:</label>
        <input type="text" placeholder="Pikachu" v-model="nuevoPokemon" />
        <button class="btn btn-primary" @click="getPokemonData">Buscar</button>
      </div>
    </div>
    <div class="row text-center">
      <div class="col">
        <img :src="pokemonData.sprites.front_default" :alt="pokemonData.name" />
      </div>
    </div>
    <div class="row text-center">
      <div class="col">
        <h2>Movimientos</h2>
        <p>
          {{ moves }}
        </p>
      </div>
    </div>
    <div class="row text-center">
      <div class="col">
        <h2>Habilidades</h2>
        <p>{{ abilities }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data: () => ({
    nuevoPokemon: "pikachu",
    pokemonData: [],
  }),
  created() {
    this.getPokemonData();
  },
  methods: {
    getPokemonData() {
      fetch(`https://pokeapi.co/api/v2/pokemon/${this.nuevoPokemon}`)
        .then((response) => response.json())
        .then((data) => (this.pokemonData = data));
    },
  },
  computed: {
    imgPokemon() {
      let image = this.pokemonData.sprites.front_default;
      return image;
    },
    moves() {
      let moves = this.pokemonData.moves
        .map((move) => move.move.name)
        .join(", ");
      return moves;
    },
    abilities() {
      let abilities = this.pokemonData.abilities
        .map((ability) => ability.ability.name)
        .join(", ");
      return abilities;
    },
  },
};
</script>

<style>
.logo {
  width: 40%;
}
.titulo {
  font-size: 3rem;
}
</style>
