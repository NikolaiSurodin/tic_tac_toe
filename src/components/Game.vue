<template>
  <div class="game">
    <div class="game-area">

      <board :cell-list="cellList"
             :winner-combination="winnerCombination"
             @clickOnCell="clickOnCell"/>

      <div class="game-info">
        <p v-if="step === 0">
         '{{ currentPlayer }}', начинайте!
        </p>
        <div class="game-info-restart" v-else-if="!!winnerCombination">
          <p v-if="currentPlayer === 'O'">Победил '{{ currentPlayer }}'</p>
          <p v-if="currentPlayer === 'X'">В этой партии победил '{{ currentPlayer }}'</p>
        </div>

        <div class="game-info-restart" v-else-if="step > 8">
          <p>Ничья!</p>

        </div>
        <p v-else>
          Продолжаем.. теперь сыграет '{{ currentPlayer }}'
        </p>
        <button class="btn" @click="restart" v-if="!!winnerCombination || step > 8 ">Еще раз!</button>
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
      step: 0,
      currentPlayer: 'X',
      winnerCombination: null
    }
  },
  methods: {
    restart() {
      this.cellList = Array( 9 ).fill( '' )
      this.step = 0
      this.winnerCombination = null
    },
    clickOnCell(i) {
      if ( this.cellList[i] || this.winnerCombination )
        return
      this.$set( this.cellList, i, this.currentPlayer )
      if ( !this.winner() ) {
        this.step++
        this.currentPlayer = this.currentPlayer === 'X' ? 'O' : 'X'
      }
    },
    winner() {
      if ( !this.winnerCombination ) {
        let cellList = this.cellList
        let allWinnerCombination = [
          [ 0, 1, 2 ], [ 3, 4, 5 ], [ 6, 7, 8 ], [ 0, 3, 6 ], [ 1, 4, 7 ],
          [ 2, 5, 8 ], [ 0, 4, 8 ], [ 2, 4, 6 ]
        ]
        for (let i = 0; i < allWinnerCombination.length; i++) {
          let [ a, b, c ] = allWinnerCombination[i]
          if ( cellList[a] && cellList[a] === cellList[b] && cellList[a] === cellList[c] ) {
            this.winnerCombination = [ a, b, c ]
            return true
          }
        }
      } else {
        return false
      }
    }
  }
}
</script>

<style scoped>
.game {
  display: flex;
  justify-content: center;
  align-items: center;
}

.game-area {
  display: flex;
  flex-flow: column;
}

.game-info {
  margin: 10px 0;
  padding: 14px 7px;
  font-size: 21px;
  box-shadow: -17px -3px 25px #0001, 0 1px 6px #0004;
  border-radius: 5px;
  display: flex;
  flex-direction: column;
}

.game-info p {
  margin: 0;
  display: flex;
  justify-content: center;
  align-items: center;
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

.game-info button:hover {
  background-color: #9eff9e;
}

.btn {
  font-weight: 600;
  font-size: 18px;
  padding: .5rem 1rem;
  margin: 0 6px;
  border: 2px solid #fff;
  border-radius: 5px;
  cursor: pointer;
  transition: all .25s ease;
}

.game-info-restart {
  display: flex;
  flex-direction: column;
}
</style>