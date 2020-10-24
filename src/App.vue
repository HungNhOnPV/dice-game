<template>
  <div class="wrapper clearfix">
    <players :activePlayer="activePlayer" :scoresPlayer="scoresPlayer" :currentScore="currentScore" :isWinner="isWinner" :finalScore="finalScore" />
    <controls @handleNewGame="handleNewGame" @handleRollDice="handleRollDice" @handleHoldScore="handleHoldScore" @handleFinalScore="handleFinalScore" />
    <dices :dices="dices" />
    <popup-rule :isOpenPopup="isOpenPopup" @handleClosePopup="handleClosePopup" />
  </div>
</template>

<script>
import Players from './components/Players'
import Controls from './components/Controls'
import Dices from './components/Dices'
import PopupRule from './components/PopupRule'
export default {
  name: 'App',
  data () {
    return {
      isPlaying: false,
      isOpenPopup: false,
      activePlayer: 0,
      scoresPlayer: [0, 0],
      dices: [1, 1],
      currentScore: 0,
      finalScore: 0,
      isWinner: 0
    }
  },
  methods: {
    handleNewGame: function () {
      this.isOpenPopup = true
    },
    handleClosePopup: function () {
      this.isOpenPopup = false
      this.isPlaying = true
      this.activePlayer = 0
      this.scoresPlayer = [0, 0]
      this.dices = [1, 1]
      this.currentScore = 0
    },
    handleRollDice: function () {
      if (!this.isPlaying || !this.finalScore) {
        alert('Bạn cần phải bấm vào nút new game và nhập final score để chơi!')
      } else {
        let dice1 = Math.floor((Math.random() * 6) + 1)
        let dice2 = Math.floor((Math.random() * 6) + 1)
        this.dices = [dice1, dice2]
        if (dice1 === 1 || dice2 === 1) {
          this.currentScore = 0
          this.activePlayer ? this.activePlayer = 0 : this.activePlayer = 1
          alert('Người chơi đã quay vào xúc sắc số 1!')
        } else {
          this.currentScore = this.currentScore + dice1 + dice2
        }
      }
    },
    handleHoldScore: function () {
      if (!this.isPlaying || !this.finalScore) {
        alert('Bạn cần phải bấm vào nút new game và nhập final score để chơi!')
      } else {
        this.scoresPlayer[this.activePlayer] = this.currentScore
        if (this.scoresPlayer[this.activePlayer] >= this.finalScore) {
          this.isWinner = this.activePlayer + 1
          this.isPlaying = false
          this.activePlayer = -1
        } else {
          this.activePlayer ? this.activePlayer = 0 : this.activePlayer = 1
          this.currentScore = 0
        }
      }
    },
    handleFinalScore: function (value) {
      this.finalScore = value
    }
  },
  components: {
    Players,
    Controls,
    Dices,
    PopupRule
  }
}
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
    background-image: linear-gradient(rgba(62, 20, 20, 0.4), rgba(62, 20, 20, 0.4)), url(./assets/back.jpg);
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
