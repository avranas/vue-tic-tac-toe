<script lang="ts">
import { ref } from 'vue'
import { defineComponent } from 'vue'
import uuid4 from 'uuid4'
import RowComponent from './RowComponent.vue'

const boardState = ref([
  ['-', '-', '-'],
  ['-', '-', '-'],
  ['-', '-', '-']
])
const message = ref('')
const turn = ref('X')
const gameOver = ref(false);

let turnCount = 0
const winningConditions = [
  [0, 1, 2],
  [3, 4, 5],
  [6, 7, 8],
  [0, 3, 6],
  [1, 4, 7],
  [2, 5, 8],
  [0, 4, 8],
  [2, 4, 6]
]
const rowsData = boardState.value.map((e) => {
  return {
    rowState: e,
    id: uuid4()
  }
})

export default defineComponent({
  name: 'BoardComponent',
  components: { RowComponent },
  data() {
    return {
      RowComponents: rowsData,
      turn: turn,
      message: message,
      gameOver: gameOver
    }
  },
  setup() {},
  methods: {
    handleClick(x: number, y: number) {
      if (boardState.value[x][y] !== '-') return
      if (gameOver.value) return
      boardState.value[x][y] = turn.value
      const test: string[] = []
      for (let x = 0; x < boardState.value.length; x++) {
        for (let y = 0; y < boardState.value[x].length; y++) {
          test.push(boardState.value[x][y])
        }
      }
      winningConditions.forEach((c) => {
        if (
          test[c[0]] === test[c[1]] &&
          test[c[1]] === test[c[2]] &&
          test[c[0]] === test[c[2]] &&
          test[c[0]] !== '-'
        ) {
          message.value = `${turn.value} wins!`
          gameOver.value = true
        }
      })
      turn.value = turn.value === 'X' ? 'O' : 'X'
      turnCount++
      if (turnCount === 9) {
        gameOver.value = true
        message.value = 'Draw!'
      }
    }
  }
})
</script>

<template>
  <div id="board">
    <div v-for="(row, index) in RowComponents" :key="row.id">
      <RowComponent :rowIndex="index" :rowState="row.rowState" :handleClick="handleClick" />
    </div>
    <p v-if="!gameOver">Turn: {{ turn }}</p>
    <p>{{ message }}</p>
  </div>
</template>

<style>
#board {
  background-color: red;
  width: 9rem;
  height: 9rem;
}
</style>
