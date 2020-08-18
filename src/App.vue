<template>
  <div id="app">
    <div id="nav">
      <router-link :to="{name: 'Home'}">Search games
        <span>
          🎮
        </span>
      </router-link>
      <router-link :to="{name: 'Stores'}">Stores
        <span>
          🏢
        </span>
      </router-link>
      <router-link :to="{name: 'About'}">About this
        <span>
          ❓
        </span>
      </router-link>
    </div>
    <router-view/>
    <footercustom/>
  </div>
</template>

<script>
import footercustom from '@/components/FooterCustom.vue'

  export default {
    components: {
      footercustom
    }
  }
</script>

<style lang="scss">
@import "css/responsive";
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

html {
  background: #1b262c;
  scroll-behavior: smooth;
}

* {
  font-family: 'Poppins', sans-serif;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-bottom: 35px;
}

#nav {
  padding: 1rem;
  @include xs-screen {
    padding: 0.3rem;
    font-size: 0.8rem;
  }
  span {
    display: none;
  }

  a {
    font-weight: bold;
    color: #0f4c75;
    padding: 0.667rem;
    text-decoration: none;
    @include xs-screen {
      padding: 0.367rem;
    }

    &.router-link-exact-active {
      color: #00b7c2;
      span {
        display: inline-block;
      }
    }
  }
}
</style>
