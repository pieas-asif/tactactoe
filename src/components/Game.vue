<template>
  <div class="body">
    <div class="board" id="board">
      <div
        v-for="i in FIELDS"
        v-bind:key="i.id"
        class="cell"
        v-bind:class="CHECKED[i]"
        @click="placeTile(i)"
        data-cell
      ></div>
    </div>
    <div class="winning-message" id="winningMessage">
      <div data-winning-message-text></div>
      <button id="restartButton" @click="restart">Restart</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Game",
  data: function () {
    return {
      X_CLASS: "x",
      O_CLASS: "o",
      WINNING_COMBINATIONS: [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
      ],
      FIELDS: [0, 1, 2, 3, 4, 5, 6, 7, 8],
      CHECKED: ["", "", "", "", "", "", "", "", ""],
      o_current: true,
    };
  },
  methods: {
    restart: function () {
      for (var i = 0; i < this.CHECKED.length; i++) {
        this.CHECKED[i] = "";
      }
    },
    placeTile: function (i) {
      console.log("Calling Placetile");
      console.log(i);
      if (this.CHECKED[i] != "") {
        return;
      } else {
        this.$set(
          this.CHECKED,
          i,
          this.o_current ? this.O_CLASS : this.X_CLASS
        );
        this.o_current = !this.o_current;
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.board {
  width: 100vw;
  height: 100vh;
  display: grid;
  justify-content: center;
  align-content: center;
  justify-items: center;
  align-items: center;
  grid-template-columns: repeat(3, auto);
}

/* game board */

.cell {
  width: var(--box-size);
  height: var(--box-size);
  border: 5px solid #eadbf4;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  cursor: pointer;
}

.cell:first-child,
.cell:nth-child(2),
.cell:nth-child(3) {
  border-top: none;
}

.cell:nth-child(3n + 3) {
  border-right: none;
}

.cell:nth-child(3n + 1) {
  border-left: none;
}

.cell:last-child,
.cell:nth-child(8),
.cell:nth-child(7) {
  border-bottom: none;
}

.cell.o,
.cell.x {
  cursor: not-allowed;
}

/* x's */

.cell.x::before,
.cell.x::after,
.board.turn-x .cell:not(.x):not(.o):hover::before,
.board.turn-x .cell:not(.x):not(.o):hover::after {
  content: "";
  position: absolute;
  width: calc(var(--player-sign-size) * 0.22);
  height: var(--player-sign-size);
  background-color: #eadbf4;
}

.cell.x::before,
.board.turn-x .cell:not(.x):not(.o):hover::before {
  transform: rotate(45deg);
}

.cell.x::after,
.board.turn-x .cell:not(.x):not(.o):hover::after {
  transform: rotate(-45deg);
}

/* circles */

.cell.o::before,
.cell.o::after,
.board.turn-o .cell:not(.x):not(.o):hover::before,
.board.turn-o .cell:not(.x):not(.o):hover::after {
  content: "";
  position: absolute;
  border-radius: 50%;
}

.cell.o::before,
.board.turn-o .cell:not(.x):not(.o):hover::before {
  width: calc(var(--player-sign-size) * 0.9);
  height: calc(var(--player-sign-size) * 0.9);
  background-color: #eadbf4;
}

.cell.o::after,
.board.turn-o .cell:not(.x):not(.o):hover::after {
  width: calc(var(--player-sign-size) * 0.5);
  height: calc(var(--player-sign-size) * 0.5);
  background-color: #e43a15;
}

/* restart button */

.winning-message {
  font-family: "Courier New", Courier, monospace;
  display: none;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgb(0, 0, 0);
  justify-content: center;
  align-items: center;
  color: white;
  font-size: 2rem;
  flex-direction: column;
}

.winning-message button {
  font-size: 3rem;
  padding-top: 3rem;
  background-color: white;
  border: 1px solid black;
  padding: 0.25em 0.5em;
  cursor: pointer;
}

.winning-message button:hover {
  background-color: #e43a15;
  border-color: white;
  color: white;
}

.winning-message.show {
  display: flex;
}
</style>
