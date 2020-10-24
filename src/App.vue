<template>
  <div class="wrapper clearfix">
    <players :activePlayer="activePlayer" :scoresPlayer="scoresPlayer" :currentScore="currentScore" />
    <controls @handleNewGame="handleNewGame" />
    <dices />
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
      scoresPlayer: [13, 30],
      currentScore: 0
    }
  },
  methods: {
    handleNewGame: function () {
      this.isOpenPopup = true
      this.isPlaying = true
    },
    handleClosePopup: function () {
      this.isOpenPopup = false
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
