<template >
  <div id="app" class="container">
    <img src="./assets/logo.png">
    <HelloWorld
        msg="Welcome to Your Vue.js App"/>
    <TicTacTable></TicTacTable>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import TicTacTable from './components/TicTacTable'

export default {
  name: 'app',
  components: {
    HelloWorld,
    TicTacTable
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
