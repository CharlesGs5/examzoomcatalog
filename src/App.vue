<template>
  <div id="app">
    <HelloWorld></HelloWorld>
    <LoginComponent></LoginComponent>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import LoginComponent from './components/LoginComponent';

export default {
  name: 'App',
  components: {
    HelloWorld,
    LoginComponent
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
