<template >
  <div id="app" class="container">
    <img src="./assets/logo.png">
    <HelloWorld
        msg="Welcome to Your Vue.js App"/>
    <TicTacGame></TicTacGame>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import TicTacGame from './components/TicTacGame'

export default {
  name: 'app',
  components: {
    HelloWorld,
    TicTacGame
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
