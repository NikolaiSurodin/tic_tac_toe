<template>
  <div class="cell"
       :class="[ value, { 'winner': winner } ]"
       :disabled="disabled"
       @click="click">{{ value }}
  </div>
</template>

<script>
export default {
  name: 'Cell',
  props: {
    value: String,
    winner: Boolean,
    disabled: Boolean
  },
  methods: {
    click() {
      this.$emit( 'click' )
    }
  }
}
</script>

<style scoped>
.cell {
  background: #fff9;
  border: 1px solid #fffc;
  font-size: 15vmin;
  font-weight: bold;
  line-height: 34px;
  padding: 0;
  text-align: center;
  box-shadow: inset 0 0 0 #0004;
  text-shadow: -1px -1px 1px #000b, -1px 1px 1px #000b, 1px -1px 1px #000b, 1px 1px 1px #000b;
  transition: all .25s ease;
  outline: none;
  cursor: pointer;
}

.cell.winner {
  background: #ff000091;
}


.cell:not([disabled]):empty:active {
  box-shadow: inset 0 2px 50px #0008;
}

.cell.X {
  color: #000000;
}

.cell.O {
  color: #000000;
}
</style>