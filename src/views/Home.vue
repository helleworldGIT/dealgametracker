<template>
  <div>
    <vue-headful
        title="Sale game garden | Home"
        description="Sale game garden | A side-project. You can search best and cheap game deals here."
    />
    <h1>
      Sale game garden🌱
    </h1>
    <div v-show="intro" class="intro">
      <p>
        Hey there! 👋
      </p>
      <p>
        Looking for the <b>cheapest deals</b> in PC games?
      </p>
      <p>
        Try searching your game here! 👇
      </p>
    </div>
    <!-- BUSCADOR -->
    <div class="buscador">
      <input v-on:keyup.enter="searchGame()" id="search" placeholder="Search a game by name🔮" v-model="search">
      <input v-on:keyup.enter="searchGame()" id="price" placeholder="Minimum price (optional)💲" v-model="price">
      <button @click="searchGame()">
        Search
      </button>
      <p class="latest" v-show="latest">
        Last search:
        {{lastSearch}} · {{lastPrice}}
      </p>
    </div>
    <!-- /BUSCADOR -->
    <!-- SPINNER -->
    <spinner v-show="seeSpinner"/>
    <!-- /SPINNER -->
    <!-- MENSAJE DE ERROR SI NO SE ENCUENTRAN JUEGOS -->
    <div v-show="errorMsg">
      <h1>
        No games found... :(
      </h1>
    </div>
    <!-- JUEGOS RESULTADOS DE LA BÚSQUEDA -->
    <gamescard :games="games" :showData="showData"></gamescard>
    <!-- /JUEGOS RESULTADOS DE LA BÚSQUEDA -->
  </div>
</template>

<script>
// @ is an alias to /src
import gamescard from '@/components/GamesCard.vue'
import spinner from '@/components/Spinner.vue'
// axios
import axios from "axios";

export default {
  name: 'Home',
  components: {
    gamescard, spinner
  },
  data(){
    return {
      // VARIABLE DE LA BÚSQUEDA
      search: '',
      // VARIABLE PARA GUARDAR LOS RESULTADOS DE LA BÚSQUEDA
      games: [],
      price: null,
      lastSearch: '',
      lastPrice: null,
      latest: false,
      // VARIABLE PARA CONTROLAR LA VISIBILIDAD DEL SPINNER,
      showData: false,
      seeSpinner: false,
      errorMsg: false,
      intro: true,
      baseURL: 'https://www.cheapshark.com/api/1.0/deals'
    }
  },
  methods: {
    // FUNCIÓN QUE BUSCA JUEGOS POR TÍTULO, LLAMADA DESDE EL BOTÓN DE BÚSQUEDA O EL ENTER
    async searchByName(){
      this.assignData()
        try {
          const response = await axios.get(`${this.baseURL}?title=${newSearch}`)
          // GUARDO LOS RESULTADOS DE LA BÚSQUEDA EN EL ARRAY 'GAMES' DEL DATA
          this.games = response.data
        } catch(err) {
          console.log(err)
        }
        this.validatingData()
    },
    // FUNCIÓN QUE BUSCA JUEGOS POR TÍTULO Y PRECIO, LLAMADA DESDE EL BOTÓN DE BÚSQUEDA O EL ENTER
    async searchByNameAndPrice(){
      this.assignData()
        try {
          const response = await axios.get(`${this.baseURL}?title=${newSearch}&upperPrice=${newPrice}`)
          // GUARDO LOS RESULTADOS DE LA BÚSQUEDA EN EL ARRAY 'GAMES' DEL DATA
          this.games = response.data
        } catch(err) {
          console.log(err)
        }
        this.validatingData()
    },
    async assignData(){
      let newPrice = this.price
      let newSearch = this.search
      this.latest = true
      this.lastSearch = this.search
      this.lastPrice = this.price
      this.price = null
      this.search = ''
    },
    async validatingData(){
      setTimeout(() =>
      {
        if(this.games.length <= 0) {
          this.errorMsg = true
          this.seeSpinner = false
          this.latest = false
        } else {
          this.seeSpinner = false
          this.showData = true
          this.latest = true
        }
      }, 1000);
    },
    async searchGame(){
      this.seeSpinner = true
      this.showData = false
      this.errorMsg = false
      this.intro = false
      if(this.price === null && this.search != "") {
        console.log('1', this.price, this.search)
        this.searchByName()
      } else if(this.price != null && this.search != "") {
        console.log('2', this.price, this.search)
        this.searchByNameAndPrice()
      } else {
        this.errorMsg = true
        this.seeSpinner = false
        this.latest = false
      }
    }
  }
}
</script>

<style lang="scss" scoped>

.latest {
  color: #318fb5;
}

.intro {
  color: #519872;
}

input, h1 {
  color: #fdcb9e;
}

input {
  border-top: 2px solid transparent;
  border-right: 2px solid transparent;
  border-left: 2px solid transparent;
  border-bottom: 2px solid #00b7c2;
  background: transparent;
  transition: .2s;
  padding: 0.667rem;
  width: auto;
  &:hover{
    border-top:  2px solid #00b7c2;
    border-right:  2px solid #00b7c2;
    border-left:  2px solid #00b7c2;
    border-radius: 5px;
    cursor: pointer;
  }
}

button {
  border: none;
  background: #00b7c2;
  color: #1b262c;
  border-radius: 15px;
  padding: 0.367rem;
  width: 80px;
  margin-left: 10px;
  transition: .2s;
  &:hover {
    background: #fdcb9e;
    cursor: pointer;
    transform: translateY(-2px);
  }
}

</style>