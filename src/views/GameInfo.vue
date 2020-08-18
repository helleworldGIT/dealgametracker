<template>
  <div class="about">
    <h1 v-if="game">{{gameName}}</h1>
    <img alt="Game cover image" title="Game cover image" :src="gameImage">
    <p>
      <b>Cheapest price ever:</b>
      💰{{gameCheapestPrice}}€
    </p>
    <p>
      🔻
    </p>
    <h3>
      Deals🔥:
    </h3>
    <div class="offers" v-for="offer in offers" :key="offer.id">
      <h3>
        Deal price:
      </h3>
      <p>
         💰{{offer.price}}€
      </p>
      <a :href="offerLink+offer.dealID">CHECK THIS DEAL</a> 
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
        console.log(response)
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
    },
    // COMPROBANDO SI HA LLEGADO LA INFO DEL JUEGO PARA PINTAR LA INFORMACIÓN O NO
    gameCheapestPrice() {
      return this.game.cheapestPriceEver ? this.game.cheapestPriceEver.price : '';
    }
  },
  created(){
    this.getParamsId()
  }
}
</script>

<style lang="scss" scoped>
@import "../css/responsive";

.offers {
  display: inline-block;
  width: 220px;
  background: #3b2e5a;
  margin: 1rem;
  border-radius: 10px;
  box-sizing: border-box;
  a {
    display: block;
    width: 100%;
    background: #251f44;
    text-decoration: none;
    font-size: 1rem;
    color: #e8505b;
    padding-top: 0.3rem;
    padding-bottom: 0.3rem;
    &:hover {
      background: #6a2c70;
    }
  }
}

h1, h3, p {
  color: #fdcb9e;
}

img {
  width: auto;
}

</style>