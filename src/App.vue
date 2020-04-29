<template>
  <div id="app">
    <h1>Vue.js and Ckeditor</h1>
    <h2>Ckeditor4</h2>
    <Ckeditor4 />
    <h2>Ckeditor5</h2>
    <Ckeditor5 />
  </div>
</template>

<script>
import Ckeditor4 from './components/Ckeditor4'
import Ckeditor5 from './components/Ckeditor5'

export default {
  name: 'App',
  components: {
    Ckeditor4,
    Ckeditor5
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
