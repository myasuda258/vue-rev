<template>
  <button>
    <span :class="value === 2 ? 'black' : 'white'" @click="onClickHandler">{{value > 0 ? text : 'x' }}</span>
  </button>  
</template>

<script lang="ts">
import { Component, Prop, Vue, Emit } from 'vue-property-decorator';

@Component
export default class CellUnit extends Vue {
  @Prop({required: true})
  public value!: number

  @Emit()
  public click(){
    console.log('emit click')
  }

  public text: string = "●"
  private onClickHandler() {
    console.log('CLICK!!', String(this.value))
    // this.color = "black"
    this.click()
  }
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
  color: red
}

</style>