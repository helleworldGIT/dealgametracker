<template>
  <div>
      <h1>
          What stores are offering these deals?
      </h1>
      <p class="info_points">
          🔴 Red points mean the store is <b>not active</b> right now,
          <br>
          🟢 green points mean they're <b>active</b>.
      </p>
      <ul>
          <li v-for="store in stores" :key="store.id">
              <h2>
              <p :class="{hide: store.isActive === 1, show: store.isActive === 0}">
                  🔴
              </p>
              <p :class="{hide: store.isActive === 0, show: store.isActive === 1}">
                  🟢
              </p>
                  {{store.storeName}}
              </h2>
          </li>
      </ul>
  </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'Stores',
    data() {
        return {
            stores: [],
            baseURL: 'https://www.cheapshark.com/api/1.0/stores',
        }
    },
    methods: {
    // FUNCIÓN QUE BUSCA LAS TIENDAS
        async searchStores(){
            try {
            const response = await axios.get(`${this.baseURL}`)
            // GUARDO LOS RESULTADOS DE LA BÚSQUEDA EN EL ARRAY 'GAMES' DEL DATA
                console.log(response)
                this.stores = response.data
                console.log('stores', this.stores)
            } catch(err) {
                console.log(err)
            }
        },
    },
    created() {
        this.searchStores()
    }
}
</script>

<style lang="scss" scoped>

.info_points {
    color: #fdcb9e;
}

.hide {
    display: none;
}

.show {
    display: inline-block;
}

h1 {
    color: #fdcb9e;
}

h2 {
    font-size: 1.2rem;
}

ul {
    list-style-type: none;
    padding-inline-start: 0;
    width:  80%;
    margin: auto;
    li {
        display: inline-block;
        padding: 0.2rem;
        margin: 0.2rem;
        color: #dddddd;
        height: 50px;
    }
}

</style>