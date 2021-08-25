<template>
  <div class="board">
    <div class="board-row" v-for="(row,key) in 3" :key="key">

      <cell v-for="i in 3"
            :key="indexInRow(i, row)"
            :symbol="cellList[indexInRow(i, row)]"
            :disabled="!winnerCombination"
            :winner="!!winnerCombination && winnerCombination.includes(indexInRow(i, row))"
            @clickOnCell="clickOnCell(i, row)"/>
    </div>
  </div>
</template>

<script>
import Cell from "@/components/Cell";

export default {
  name: 'Board',
  data() {
    return {}
  },
  props: {
    cellList: Array,
    winnerCombination: Array
  },
  components: {
    Cell
  },
  methods: {
    indexInRow(index, row, maxCount) {
      maxCount = 3
      return (row * maxCount + index) - (maxCount + 1)
    },
    clickOnCell(index, row) {
      this.$emit( 'clickOnCell', this.indexInRow( index, row ) )
    }
  }
}
</script>

<style scoped>
.board {
  background-color: #000000;
  border: 1px solid transparent;
  box-shadow: 4px -1px 25px #0004;
  border-radius: 10px;
  width: 65vmin;
  height: 65vmin;
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: repeat(3, 1fr);
}

.board-row {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: 1fr;
}
</style>