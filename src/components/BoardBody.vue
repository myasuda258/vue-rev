<template>
  <div>
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
  </div>
</template>

<script lang="ts">
export default {

}
</script>

<style>

</style>