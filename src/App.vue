<template>
  <div id="app">
    <Game />
  </div>
</template>

<script>
import Game from './components/Game.vue';

export default {
  name: 'App',
  components: {
    Game,
  },
};
</script>

<style lang="scss">
body {
  background-color: #05c4b14d;
  background: url("https://iconka.com/wp-content/uploads/edd/2017/08/meowers_preview2.png") repeat repeat;
  background-size: cover;
  margin: 0;
  padding: 0;
  max-width: 100%;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  width: 40%;
  margin: 0 auto;
}
</style>
