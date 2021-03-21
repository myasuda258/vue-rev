<template>
  <div class="hello">
    <div
      v-for="(row, rindex) in bodyValue"
      :key="rindex">
      <cell-unit
        v-for="(cell, cindex) in row"
        :key="cindex"
        :address="{x:cindex, y:rindex}"
        :value="bodyValue[rindex][cindex]"
        @onClickHandler="clickCellHandler"
      ></cell-unit>
    </div>
    <h1>{{ msg }}</h1>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue, Emit } from 'vue-property-decorator'
import CellUnit from '@/components/CellUnit.vue'
import CellAddress from '@/types/CellAddress'

@Component({
  components: {
    CellUnit,
  },
})
export default class GameBoard extends Vue {
  @Prop() private msg!: string;
  private bodyValue: number[][] = new Array()
  @Prop()
  private nextPlayer!: number

  created(){
    console.log('component created')
    this.bodyValue = 
      [
        [0,0,0,0,0,0,0,0],
        [0,0,0,0,0,0,0,0],
        [0,0,0,0,0,0,0,0],
        [0,0,0,1,2,0,0,0],
        [0,0,0,2,1,0,0,0],
        [0,0,0,0,0,0,0,0],
        [0,0,0,0,0,0,0,0],
        [0,0,0,0,0,0,0,0],
      ]
  }

  private clickCellHandler(cell: CellAddress) {
    const x = cell.x
    const y = cell.y
    console.log('hello world click handler', x, y)
    this.putStone(cell)
  }

  private putStone(cell: CellAddress) {
    const x = cell.x
    const y = cell.y
    if (this.bodyValue[y][x] > 0) {
      console.warn('this has stone already', x, y)
      return
    }
    const bodyValue_ = JSON.parse(JSON.stringify(this.bodyValue))
    bodyValue_[y][x] = this.nextPlayer
    this.bodyValue = bodyValue_
    this.toggleNextPlayer()
  }

  @Emit('toggleNextPlayer')
  private toggleNextPlayer() {}

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
