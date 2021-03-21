<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <display-next-player :next-player="nextPlayer"></display-next-player>
    <game-board
      :next-player="nextPlayer"
      msg="Welcome to Your Vue.js + TypeScript App"
      @toggleNextPlayer="toggleNextPlayer"/>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import GameBoard from './components/GameBoard.vue';
import DisplayNextPlayer from '@/components/DisplayNextPlayer.vue'

@Component({
  components: {
    GameBoard,
    DisplayNextPlayer,
  },
})
export default class App extends Vue {
  private nextPlayer: number = 1

  private toggleNextPlayer() {
    this.nextPlayer = 3 - this.nextPlayer
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
