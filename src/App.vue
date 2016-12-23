<template>
  <div id="app">
    <button @click.prevent="application='Hello'">Typing Speed practice</button>
    <button @click.prevent="application='TicTac'">Tic Tac Toe</button>
    <button @click.prevent="application='Memory'">Memory</button>
    <button @click.prevent="application='Type'">Type</button>
    <hello v-if="application=='Hello'"></hello>
    <memory v-if="application=='Memory'"></memory>  
    <type v-if="application=='Type'"></type>  
    <tic v-if="application=='TicTac'"></tic>    
  </div>
</template>

<script>
import Hello from './components/Hello'
import Tic from './components/TicTac'
import Memory from './components/Memory'
import Type from './components/Type'

export default {
  name: 'app',
  components: {
    Hello,
    Tic,
    Memory,
    Type
  },
  data: function(){
    return {application:'Hello'}
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
}
</style>
