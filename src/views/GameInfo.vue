<template>
  <div class="about">
    <h1>This is an about page</h1>
    <p v-if="game">
      nombre: {{gameName}}
    </p>
    <img :src="gameImage">
    <div class="offers" v-for="offer in offers" :key="offer.id">
      <a :href="offerLink+offer.dealID">A ver</a> <p>
        precio: {{offer.price}}
      </p>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data(){
    return {
      gameId:null,
      game: [],
      offers: [],
      offerLink: 'https://www.cheapshark.com/redirect?dealID=',
      gameImage: ''
    }
  },
  methods: {
    // RECOGIENDO LA ID QUE ME LLEGA POR PARÁMETRO DE LA VISTA
    async getParamsId(){
      try {
        this.gameId = this.$route.params.id;
        // LLAMANDO A LA FUNCIÓN QUE RECOGE LOS DATOS DEL JUEGO
        this.getGameByID();
      } catch(err) {
        console.log(err)
      }
    },
    // RECOGIENDO LA INFORMACIÓN DEL JUEGO SEGÚN LA ID QUE LLEGA A LA PÁGINA
    async getGameByID(){
      try {
        const response = await axios.get(`https://www.cheapshark.com/api/1.0/games?id=${this.gameId}`);
        this.game = response.data
        this.offers = this.game.deals
        // LLAMANDO A LA FUNCIÓN QUE RECOGE LA IMAGEN DEL JUEGO
        this.getGameImage()
      } catch(err) {
        console.log(err)
      } 
    },
    // RECOGIENDO LA IMAGEN DEL JUEGO QUE SE MUESTRA
    async getGameImage(){
      try {
        const response = await axios.get(`https://www.cheapshark.com/api/1.0/games?title=${this.game.info.title}`)
        this.gameImage = response.data[0].thumb
      } catch(err) {
        console.log(err)
      }
    }
  },
  computed: {
    // COMPROBANDO SI HA LLEGADO LA INFO DEL JUEGO PARA PINTAR LA INFORMACIÓN O NO
    gameName() {
      return this.game.info ? this.game.info.title : '';
    }
  },
  created(){
    this.getParamsId()
  }
}
</script>
