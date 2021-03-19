<template>
  <div class="hello">
    <div v-for="(row, rindex) in bodyValue" :key="rindex">
      <cell-unit v-for="(cell, cindex) in row" :key="cindex" :value="bodyValue[cindex][rindex]" @onClickHandler="clickCellHandler"></cell-unit>
    </div>
    <h1>{{ msg }}</h1>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator'
import CellUnit from '@/components/CellUnit.vue'

@Component({
  components: {
    CellUnit,
  },
})
export default class HelloWorld extends Vue {
  @Prop() private msg!: string;
  private bodyValue: number[][] = Array(8).fill(Array(8).fill(-1))

  private clickCellHandler(str: string) {
    console.log('hello world click handler', str)
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
