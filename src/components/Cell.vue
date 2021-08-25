<template>
  <div class="cell"
       :class="{ 'winner': winner } "
       :disabled="disabled"
       @click="clickOnCell">
    {{ symbol }}
  </div>
</template>

<script>
export default {
  name: 'Cell',
  props: {
    symbol: String,
    winner: Boolean,
    disabled: Boolean
  },
  methods: {
    clickOnCell() {
      this.$emit( 'clickOnCell' )
    }
  }
}
</script>

<style scoped>
.cell {
  background: rgba(0, 0, 0, 0.6);
  border: 1px solid #fffc;
  font-size: 15vmin;
  font-weight: bold;
  padding: 0;
  text-align: center;
  box-shadow: inset 0 0 0 #0004;
  transition: all .25s ease;
  outline: none;
  cursor: pointer;
  color: #ffffff;
  border-radius: 5px;
  margin: 7px 5px;
}

.cell.winner {
  background: #ff000091;
}


.cell:not([disabled]):empty:active {
  box-shadow: inset 0 2px 50px #0008;
}

.cell.X {
  color: #ffffff;
}

.cell.O {
  color: #ffffff;
}
</style>