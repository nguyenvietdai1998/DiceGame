<template>
  <div id="app">
    <div class="wrapper clearfix">
      <players
        v-bind:activePlayer="activePlayer"
        v-bind:scoresPlayer="scoresPlayer"
        v-bind:currentScore="currentScore"
      />

      <controls
        v-on:handleNewGame="handleNewGame"
        v-on:handleRollDice="handleRollDice"
        v-on:handleHoldScore="handleHoldScore"
      />

      <dices v-bind:dices="dices" />

      <popup-rule
        v-bind:isOpenPopup="isOpenPopup"
        v-on:handleConfirm="handleConfirm"
      />
    </div>
  </div>
</template>

<script>
import Players from "./components/Player.vue";
import Controls from "./components/Controls.vue";
import Dices from "./components/Dices.vue";
import PopupRule from "./components/PopupRule.vue";

export default {
  name: "app",
  data() {
    return {
      isPlaying: false,
      isOpenPopup: false,
      activePlayer: 0, // Ai là người chơi hiện tại
      scoresPlayer: [20, 55],
      currentScore: 30,
      dices: [1, 6],
    };
  },
  components: {
    Players,
    Controls,
    Dices,
    PopupRule,
  },
  methods: {
    handleNewGame() {
      console.log("handleNewGame App.vue");
      this.isOpenPopup = true;
    },

    handleConfirm() {
      console.log("handleConfirm in App.vue");
      this.isPlaying = true;
      this.isOpenPopup = false;
      this.activePlayer = 0;
      this.scoresPlayer = [0, 0];
      this.currentScore = 0;
      this.dices = [1, 1];
    },

    nextPlayer() {
      this.activePlayer = this.activePlayer == 0 ? 1 : 0;
      this.currentScore = 0;
    },

    handleRollDice() {
      console.log("handleRollDice in App.vue");
      if (this.isPlaying) {
        var dice1 = Math.floor(Math.random() * 6) + 1;
        var dice2 = Math.floor(Math.random() * 6) + 1;

        this.dices = [dice1, dice2];
        console.log(dice1, dice2);

        if (dice1 === 1 || dice2 === 1) {
          let activePlayer = this.activePlayer;
          setTimeout(function () {
            alert(
              `Người chơi Player ${
                activePlayer + 1
              } đã quay trúng số 1. Rất tiếc`
            );
          }, 10);
          this.nextPlayer();
        } else {
          this.currentScore = this.currentScore + dice1 + dice2;
        }
      } else {
        alert("Vui lòng nhấn vào nút NewGame");
      }
    },
    handleHoldScore() {
      if (this.isPlaying) {
        // this.scoresPlayer[this.activePlayer] = this.scoresPlayer;
        // [this.activePlayer] + this.currentScore;

        let { scoresPlayer, activePlayer, currentScore } = this;
        let oldScore = scoresPlayer[activePlayer];

        this.scoresPlayer[activePlayer] = oldScore + currentScore;
      } else {
        alert("Vui lòng nhấn vào nút NewGame");
      }
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.clearfix::after {
  content: "";
  display: table;
  clear: both;
}

body {
  background-image: linear-gradient(
      rgba(62, 20, 20, 0.4),
      rgba(62, 20, 20, 0.4)
    ),
    url("/public/assets/back.jpg");
  background-size: cover;
  background-position: center;
  font-family: Lato;
  font-weight: 300;
  position: relative;
  height: 100vh;
  color: #555;
}

.wrapper {
  width: 1000px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #fff;
  box-shadow: 0px 10px 50px rgba(0, 0, 0, 0.3);
  overflow: hidden;
}
</style>
