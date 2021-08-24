<template>
  <div class="game">
    <div class="game-area">

      <board :cell-list="cellList"
             :winner="winner"
             @click="clickOnCell"/>

      <div class="game-info">
        <p v-if="stepNumber === 0">
          Играет {{ currentPlayer }}
        </p>
        <p v-else-if="!!winner">
          Победил {{ currentPlayer }}
          <button @click="restart">Еще раз</button>
        </p>
        <p v-else-if="stepNumber > 8">
          Ничья
          <button @click="restart">Еще раз</button>
        </p>
        <p v-else>
          еще раз {{ currentPlayer }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import Board from "@/components/Board"

export default {
  name: 'Game',
  components: {
    Board
  },
  data() {
    return {
      cellList: Array( 9 ).fill( '' ),
      stepNumber: 0,
      currentPlayer: 'X',
      winner: null
    }
  },
  methods: {
    restart() {
      console.log( 'restart' )
    },
    clickOnCell() {
      console.log( 'clickOnCell' )
    }
  }
}
</script>

<style scoped>
.game {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.game-area {
  display: flex;
  flex-flow: column;
}

.game-info {
  margin: 10px 0px;
  padding: 14px 7px;
  font-size: 21px;
  box-shadow: -17px -3px 25px #0001, 0 1px 6px #0004;
  border-radius: 5px;
}

.game-info p {
  margin: 0;
  display: flex;
  justify-content: center;
  align-items: center;
}

.game-info b {
  padding: 0 5px;
}

.game-info button {
  font-weight: 600;
  font-size: 18px;
  padding: .5rem 1rem;
  margin: 0 6px;
  border: 2px solid #fff;
  border-radius: 5px;
  cursor: pointer;
  transition: all .25s ease;
}

</style>