<template>
  <div id="app">
    <Game />
  </div>
</template>

<script>
import Game from './components/Game.vue'

export default {
  name: 'TacTacToe',
  components: {
    Game
  }
}
</script>

<style>
*, *::after, *::before {
    box-sizing: border-box;
}

:root {
    --box-size: 100px;
    --player-sign-size: calc(var(--box-size) * .8);
}

body {
    margin: 0;
    background: #e43a15;
    background: -webkit-linear-gradient(to right, #e65245, #e43a15);
    background: linear-gradient(to right, #e65245, #e43a15);
}
</style>
