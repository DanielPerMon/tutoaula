<template>
  <div class="head">
    <input
      type="text"
      v-model="id"
      name="pokemon"
      autocomplete="off"
      @onsubmit="getPokemon"
    />
    <button @click="getPokemon()">Buscar</button>
    <div class="poke-card">
      <div v-if="name == ''">Pokedex</div>
      <div v-else>{{ name }}</div>
      <div
        class="img-container"
        v-if="name == '' || name == 'No encontramos ese pokemon'"
      >
        <img class="poke-img" src="./assets/poke-shadow.png" />
      </div>
      <div class="img-container" v-else>
        <img class="poke-img" :src="gif" :alt="name" />
      </div>
      <div>
        <span>{{ id }}</span>
      </div>
      <div v-if="tipos != ''">
        <div v-for="(type, i) in tipos" :key="i">
          <div class="poke-types" v-bind:style="{color: typeColors[type]}">
            {{ type }}
          </div>
        </div>
      </div>
      <div v-if="stats != ''">
        <div v-for="(item,i) in stats" :key="i">
          <div class="poke-stats">
            {{item.nombre}}
          </div>
          <div class="poke-stats">
            {{item.puntos}}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
var audio = new Audio("./Deoxys.mp3");

export default {
  name: "gif",
  data() {
    return {
      id: "",
      name: "",
      gif: "",
      pokemon: [],
      tipos: [],
      typeColors: {
        normal: "#B09398",
        fire: "#FF675C",
        water: "#0596C7",
        grass: "#4A9681",
        electric: "#FFEA70",
        ice: "#AFEAFD",
        fighting: "#2F2F2F",
        poison: "#795663",
        ground: "#D2B074",
        flying: "#7AE7C7",
        psychic: "#FFC6D9",
        bug: "#A2FAA3",
        rock: "#999799",
        ghost: "#561D25",
        dark: " #492725",
        dragon: "#DA627D",
        steel: "#1D8A99",
        fairy: " #edb4b0 ",
      },
      stats:[]
    };
  },
  methods: {
    getPokemon() {
      const axiosInstance = axios.create({
        headers: {
          "Access-Control-Allow-Origin": "*",
        },
      });
      axiosInstance
        .get(`https://pokeapi.co/api/v2/pokemon/${this.id}`)
        .then((response) => {
          this.pokemon = response.data;
          console.log(this.pokemon);
          const { name, types, stats } = response.data;
          this.name = name;
          console.log("soy el name de data: " + this.name);
          this.tipos = types.map(function(tipo){
            return tipo.type.name
          })
          this.stats = stats.map(function(stat){
            return{
              nombre: stat.stat.name,
              puntos: stat.base_stat
            }
          })
          this.gif =
            "http://play.pokemonshowdown.com/sprites/xyani/" + name + ".gif";
          console.log(this.stats)
        })
        .catch((err) => this.noEncontrado());
      this.tipos = [];
    },
    noEncontrado() {
      this.name = "No encontramos ese pokemon";
    },
  },
  created() {
    audio.pause();
    audio.play();
    audio.loop = true;
  },
};
</script>

<style>
</style>
