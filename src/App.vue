<template>
  <div id="app">
    <!-- Cabecera -->
    <header>
      <img alt="Poke-logo" src="./assets/pokemon-logo.png">
      <h1 class="title">Bienvenidos a la PokeGuía</h1>
      <div class="pokeball">
        <img class="poke1" src="./assets/pokeball1.png" alt="Pokeball">
      </div>
    </header>
    <!-- Sección barra de busqueda -->
    <main>
      <label class="name-title">Nombre: </label>
      <input class="poke-name" type="text" v-model="pokemon.name">
      <button class="poke-search" @click="search">Buscar</button>
    </main>
    <!-- Sección de información del pokémon -->
    <section>
      <div class="img-container">
        <img class="imagePoke" :src="pokeImg">
      </div>
      <h2 class="subtitle-move">Movimientos</h2>
      <ol class="list-one">
        <li class="move-list" v-for="move in pokeMoves" :key = move>{{move.move.name}}</li>
      </ol>
      <h2 class="subtitle-abilities">Habilidades</h2>
      <ol class="list-two">
        <li class="abilities-list" v-for="abilitie in pokeAbilities" :key = "abilitie">{{abilitie.ability.name}}</li>
      </ol>
    </section>
    <!-- Sección de cierre -->
    <footer>
      <img class="poke-footer" src="./assets/team-icons.png" alt="">
    </footer>
  </div>
</template>

<script>
export default {
  data() {
    return {
      pokemon: {
        name: 'pikachu',
        moves: [],
        abilities: []
      }
    }
  },
  methods: {
    search() {
      let name = this.pokemon.name.toLowerCase()
      fetch(`https://pokeapi.co/api/v2/pokemon/${name}`)
      .then(response => response.json())
      .then(response => this.pokemon = response)
    }
  },
  created() {
    this.search()
  },
  computed: {
    pokeImg() {
      return this.pokemon.sprites.front_default;
    },
    pokeMoves() {
      return this.pokemon.moves;
    },
    pokeAbilities() {
      return this.pokemon.abilities;
    }
  }
}
</script>

<style>
  body {
    background-color: #000;
    color: #FFF;
    margin: 0; 
  }
  #app {
    font-family: 'Handlee', cursive;
    text-align: center;
    margin-top: 2em;
  }
  /* cabecera donde esta la imagen, título, y la barra de busqueda */
  img {
    margin: 0 auto;
    width: 30%;
  }
  .title {
    font-size: 3em;
  }
  .poke1 {
    width: 3em;
    margin-bottom: 2em;
  }
  .name-title {
    font-size: 1.5em;
    font-weight: bold;
  }
  .poke-name {
    background-color: yellow;
    text-align: center;
    font-size: 1em;
    font-weight: bold;
    padding: 0.5em;
    border: 1px solid #000000;
    border-radius: 2em;
    margin-left: 1em; 
  }
  .poke-search {
    width: 7em;
    background-color: blue;
    color: #FFFFFF;
    font-size: 1em;
    font-weight: bold;
    padding: 0.5em;
    border-radius: 2em;
    border: none;
    margin-left: 1em;
    transition: .5s;
  }
  .poke-search:hover {
    background-color: red;
    border: 1px solid blue;
  }
  /* imagen del pokémon que se muestra de fondo */
  .imagePoke {
    width: 20%;
  }
  /* Lista de movimientos y habilidades */
  ol {
    padding: 0;
  }
  .list-two {
    margin-bottom: 3em;
  }
  .subtitle-move, .subtitle-abilities {
    font-size: 3em;
    font-weight: bold;
    text-decoration: underline;
  }
  .subtitle-abilities {
    margin-top: 1.5em;
  }
  .move-list, .abilities-list {
    color: #FFFFFF;
    list-style: none;
    font-size: 2em;
    padding: 0.5em;
  }
  /* Cierre */
  footer {
    background-color: darkred;
  }
  .poke-footer {
    width: 20%;
    margin-top: 1em;
    margin-bottom: 1em;
  }
</style>
