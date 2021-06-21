<template>
  <div id="app">
    <!--img alt="Vue logo" src="./assets/logo.png"-->
    <MessageTransformer msg="Message Transformer"/>
  </div>
</template>

<script>
import MessageTransformer from './components/MessageTransformer.vue'

export default {
  name: 'App',
  components: {
    MessageTransformer
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
