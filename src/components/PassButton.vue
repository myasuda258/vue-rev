<template>
  <p>
    <button @click="confirmPass">Pass</button>
  </p>
</template>

<script lang="ts">
import { Component, Vue, Emit } from 'vue-property-decorator';

@Component
export default class DisplayNextPlayer extends Vue {
  @Emit('toggleNextPlayer')
  private toggleNextPlayer() {}

  private confirmPass() {
    if (confirm('pass?')) {
      console.log('pass')
      this.toggleNextPlayer()
    } else {
      console.log('cancel pass')
    }
  
  }

}
</script>

<style scoped>

</style>