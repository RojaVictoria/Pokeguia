<template>
  <div id="app">
    <img src="./assets/logo-pokemon.png" alt="" class="logo">
    <h1>PokeGuía</h1>
    <div>
      <label>Nombre: </label>
      <input v-model="nombrePokemon" placeholder="Ingrese un pokemon">
      <button @click="buscarPokemon">Buscar</button>
    </div>
    <div>
      <img :src="datosPokemon.sprites.front_default">
      <h2>Movimientos</h2>
      <span v-for="(move, $index) in moves" :key="$index"> 
        {{ move.move.name }}; 
      </span>
      <h2>Habilidades</h2>
      <span v-for="(ability, $index) in abilities" :key="$index"> 
        {{ ability.ability.name }}; 
      </span>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data: () => ({
    nombrePokemon: "",
    datosPokemon: [],
  }),
  created() {
    this.nombrePokemon = "pikachu";
    this.buscarPokemon();
  },
  methods: {
    buscarPokemon(){
      fetch(`https://pokeapi.co/api/v2/pokemon/${this.nombrePokemon}`)
      .then(response => response.json())
      .then(data => this.datosPokemon = data)
    }
  },
  computed: {
    moves(){
      return (this.datosPokemon.moves)
    },
    abilities(){
      return (this.datosPokemon.abilities)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  margin: 20px;

}

.logo {
  width: 40%;
}
</style>
