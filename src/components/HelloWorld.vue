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
import { Component, Prop, Vue } from 'vue-property-decorator'
import CellUnit from '@/components/CellUnit.vue'
import CellAddress from '@/types/CellAddress'

@Component({
  components: {
    CellUnit,
  },
})
export default class HelloWorld extends Vue {
  @Prop() private msg!: string;
  private bodyValue: number[][] = // Array(8).fill(Array(8).fill(-1))
    [[0,0,0,0,0,0,0,0],
    [0,0,0,0,0,0,0,0],
    [0,0,0,0,0,0,0,0],
    [0,0,0,0,0,0,0,0],
    [0,0,0,0,0,0,0,0],
    [0,0,0,0,0,0,0,0],
    [0,0,0,0,0,0,0,0],
    [0,0,0,0,0,0,0,0],
    ]

  created(){
    console.log('component created')
    this.bodyValue[3][3] = 1
    this.bodyValue[4][4] = 1
    this.bodyValue[3][4] = 2
    this.bodyValue[4][3] = 2
  }

  private clickCellHandler(cell: CellAddress) {
    const x = cell.x
    const y = cell.y
    console.log('hello world click handler', x, y)
    const bodyValue_ = JSON.parse(JSON.stringify(this.bodyValue))
    if (bodyValue_[y][x] === 1) {
      bodyValue_[y][x] = 2
    } else {
      bodyValue_[y][x] = 1
    }
    this.bodyValue = bodyValue_
  }
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
