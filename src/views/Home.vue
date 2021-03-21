<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <GameBoard msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import GameBoard from '@/components/GameBoard.vue'

export default {
  name: 'Home',
  components: {
    GameBoard,
  },
}
</script>
