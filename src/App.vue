<template>
  <div>
    <header>
      <h1>POKEMON</h1>
    </header>
    <div class="pokemondiv">
      <div class="card" v-for="pokemon in pokemons" :key="pokemon.id">
        <img :src="pokemon.imagen" alt="imagen de {{ pokemon.nombre }}" />
        <h2>{{ pokemon.nombre }}</h2>
        <div class="pkemones" :style="{ backgroundColor: pokemon.type_color }">
          {{ pokemon.type_name }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      pokemons: []
    };
  },
  mounted() {
    this.pokemones();
  },
  methods: {
    async pokemones() {
      try {
        const response = await axios
        .get('https://cobuses.com.co/APIV2/model/pokemon.php?dato=getallpokemon');

        this.pokemons = response.data;
      } catch (err) {
        console.error('error en la api:', err);
      }
    }
  }
};
</script>

<style>
* {
  margin: 0;
}

header {
  background: purple;
  color: yellow;
  width: 100%;
  height: 100px;
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2rem;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
}

.pokemondiv {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 20px;
  padding: 20px; 
}

.card {
  background: #f9f9f9;
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 10px;
  text-align: center;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.card img {
  width: 100%;
}

.pkemones {
  margin-top: 10px;
  padding: 5px;
  border-radius: 4px;
  color: #fff;
  font-weight: bold;
}
img{
  height: 26rem;
  object-fit: cover;
  object-position: center center;
  background: #EDEDED;
  border-radius: 5px;
}
</style>
