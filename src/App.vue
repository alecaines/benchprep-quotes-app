<template>
  <div id="app">
  <link href='https://fonts.googleapis.com/css?family=Didact Gothic' rel='stylesheet'>    
    <div class="title-bar">
      <h1>Quotes App</h1>
    </div>
    <br><br><br>
    <Quotes msg="Quotes"/>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Quotes from './components/Quotes'
export default {
  name: 'App',
  components: {
    Quotes
  }
}
</script>

<style>
#app {
  /* font-family: Avenir, Helvetica, Arial, sans-serif; */
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  font-family: 'Didact Gothic';

}

.title-bar{
  background-color:#ebe6e6;
  position: absolute;
  display: inline-block;
  left: 0%;
  right: 0%;
  top: 0%;
}
</style>
