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

  public created() {
    console.log('component created')
    this.bodyValue =
      [
        [0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 1, 2, 0, 0, 0],
        [0, 0, 0, 2, 1, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0],
      ]
  }

  private clickCellHandler(cell: CellAddress) {
    const cells = this.generateTurnCellArray(cell)
    if (cells.length > 2) {
      this.putStone(cells)
    } else {
      console.warn('this does not have stone around', cells[0].x, cells[0].y)
    }
  }

  private putStone(cells: CellAddress[]) {
    const bodyValue_ = JSON.parse(JSON.stringify(this.bodyValue))
    cells.forEach(cell => {
      const x = cell.x
      const y = cell.y
      bodyValue_[y][x] = this.nextPlayer
    })
    this.bodyValue = bodyValue_
    this.toggleNextPlayer()
  }

  private generateTurnCellArray(cell: CellAddress) {
    const x = cell.x
    const y = cell.y
    let returnArray = new Array()
    if (this.bodyValue[y][x] > 0) {
      console.warn('this has stone already', x, y)
      return returnArray
    }

    const around = [-1, 0, 1]
    around.forEach(dy => {
      if (!this.bodyValue[y+dy]) {
        return
      }
      around.forEach(dx => {
        // console.log(`this.bodyValue[${y+dy}][${x+dx}]: ${this.bodyValue[y+dy][x+dx]}`)
        // if (this.bodyValue[y+dy][x+dx] === 3 - this.nextPlayer) {
          returnArray = returnArray.concat(this.checkOneVector(cell, dx, dy))
        // }
      })      
    })
    console.log('return :::', returnArray)
    returnArray.push(cell)
    return returnArray
  }

  private checkOneVector(cell: CellAddress, dx: number, dy: number) {
    const x = cell.x
    const y = cell.y
    if (this.bodyValue[y+dy] === void(0)) {
      // 確認先が範囲外なら
      return []
    }
    if (!this.bodyValue[y+dy][x+dx]) {
      // 確認先が範囲外or空白なら
      return []
    }
    // 確認先が手番と同じ色なら
    if (this.bodyValue[y+dy][x+dx] === this.nextPlayer) {
      return [{x:x+dx, y:y+dy}]
    }
    const nextCell = {
      x: cell.x + dx,
      y: cell.y + dy,
    }
    const beforeCheckAnswer: CellAddress[] = this.checkOneVector(nextCell, dx, dy)
    if (beforeCheckAnswer.length === 0) {
      return []
    }
    beforeCheckAnswer.push(nextCell)
    return beforeCheckAnswer
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
