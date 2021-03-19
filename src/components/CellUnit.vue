<template>
  <button @click="onClickHandler">
    <span :class="value === 1 ? 'black' : (value === 2 ? 'white' : 'green')">{{text}}</span>
  </button>  
</template>

<script lang="ts">
import { Component, Prop, Vue, Emit } from 'vue-property-decorator';

@Component
export default class CellUnit extends Vue {
  @Prop({required: true})
  public value!: number
  @Prop({required: true})
  public address!: CellAddress

  private text: string = '●'
  
  // @Emit('onClickHandler')
  public click(){
    console.log('emit click')
    return 'unit'
  }

  @Emit('onClickHandler')
  private onClickHandler() {
    console.log('CLICK!!', String(this.value))
    console.log('ADDRESS ', this.address.x, this.address.y)
    // this.color = "black"
    // this.click()
    return this.address
  }
}

export interface CellAddress {
  x: number
  y: number
}
</script>

<style>
button {
  width: 40px;
  height: 40px;
  background-color: yellowgreen;
  font-size: 20pt;
}
.white {
  color: white
}
.black {
  color: black
}
.green {
  color: yellowgreen
}

</style>