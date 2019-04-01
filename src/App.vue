<template>
  <div id="app">
    <h1>Tic Tac Toe</h1>
    <h2 class="game-info">
      {{ status }}
    </h2>
    <Board
      :squares="squares"
      :handleClick="handleClick"
      :winnerList="winnerList"
    />
    <button
      @click="newGame"
      class="new-game-button"
    >
      New Game
    </button>
  </div>
</template>

<script>
import Board from './components/Board'

export default {
  name: 'app',
  components: {
    Board,
  },
  data() {
    return {
      xIsNext: true,
      squares: Array(9).fill(null),
    }
  },
  computed: {
    winnerList() {
      return calculateWinner(this.squares);
    },
    status() {
      if(this.winnerList) {
        return 'Winner: ' + this.squares[this.winnerList[0]];
      } else if(this.squares.includes(null)) {
        return 'Next player: ' + (this.xIsNext ? 'X' : 'O');
      } else {
        return 'Draw Game.';
      }
    }
  },
  methods: {
    handleClick(i) {
      if(this.squares[i] || this.winnerList) {
        return;
      } else {
        const squares = this.squares.slice();
        const xIsNext = this.xIsNext;
        squares[i] = xIsNext ? 'X' : 'O';
        this.squares = squares.slice();
        this.xIsNext = !xIsNext;
      }
    },
    newGame() {
      this.squares = Array(9).fill(null);
      this.xIsNext = true;
    }
  },
}

function calculateWinner(squares) {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6]
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return [a, b, c];
    }
  }
  return null;
}
</script>

<style>
.game-info {
  margin-bottom: 10px;
  color: #42b983;
}
.new-game-button {
  margin-top: 30px;
  border-radius: 5px;
  font-weight: bold;
  font-size: medium;
  background-color: aquamarine;
}
#app {
  text-align: center;
  font: 14px 'Century Gothic', Futura, sans-serif;
  margin: 20px;
}
</style>
