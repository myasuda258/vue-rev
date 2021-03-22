<template>
  <p>Next Player: {{ nextPlayer === 1 ? 'Black' : 'White'}}</p>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class DisplayNextPlayer extends Vue {
  @Prop({required: true})
  public nextPlayer!: number
}
</script>

<style>

</style>