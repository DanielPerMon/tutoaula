<template>
  <div class="main">
    <div class="head">
      <button @click="prev">Anterior</button>
      <span>Mostrando pokemons del {{ inicio }} al {{ fin }}</span>
      <button @click="next">Siguiente</button>
    </div>
    <br>
    <div v-for="(url,i) in indexes" :key="i" class="tarjetas">
      <card :url="url"></card>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Card from "./components/Card.vue"
var audio = new Audio("./Deoxys.mp3");

export default {
  name: "gif",
  data() {
    return {
      indexes: [],
      siguiente: "",
      anterior: "",
      inicio: 1,
      fin: 20,
      url: "https://pokeapi.co/api/v2/pokemon?offset=0&limit=20",
      stats: [],
    };
  },
  methods: {
    getIndex() {
      const axiosInstance = axios.create({
        headers: {
          "Access-Control-Allow-Origin": "*",
        },
      });
      axiosInstance
        .get(this.url)
        .then((response) => {
          this.indexes = response.data.results.map(function (data) {
            return data.url;
          });
          this.siguiente = response.data.next;
          this.anterior = response.data.previous;
          console.log(this.indexes);
        })
    },
    next() {
      if (this.fin < 900) {
        this.inicio += 20;
        this.fin += 20;
        this.url = this.siguiente;
        this.indexes=[];
        this.getIndex();
      }
    },
    prev() {
      if (this.fin > 20) {
        this.inicio -= 20;
        this.fin -= 20;
        this.url = this.anterior;
        this.indexes=[];
        this.getIndex();
      }
    }
  },
  components: {
    Card: Card
  },
  created() {
    audio.pause();
    audio.play();
    audio.loop = true;
    this.getIndex();
  },
};
</script>

<style>
</style>
