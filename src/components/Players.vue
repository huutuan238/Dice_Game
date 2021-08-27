<template>
  <div class="wrapper-player">
    <div class="player-panel" :class="{ 
      active: activePlayer == 1 && !this.isWiner,
      winner: activePlayer == 1 && this.isWiner }">
      <div class="player-name">{{ getNamePlayer(1) }}</div>
      <div class="player-score">{{ scorePlayer[0] }}</div>
      <div class="player-current-box">
        <div class="player-current-label">Current</div>
        <div class="player-current-score">{{ activePlayer == 1 ? currentScore : 0 }}</div>
      </div>
    </div>

    <div class="player-panel" :class="{ 
      active: activePlayer == 2 && !this.isWiner,
      winner: activePlayer == 2 && this.isWiner }">
      <div class="player-name">{{ getNamePlayer(2) }}</div>
      <div class="player-score">{{ scorePlayer[1] }}</div>
      <div class="player-current-box">
        <div class="player-current-label">Current</div>
        <div class="player-current-score">{{ activePlayer == 2 ? currentScore : 0 }}</div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'players',
  props: {
    currentScore: {
      type: Number,
      default: 0
    },
    scorePlayer: {
      type: Array,
      default: [0, 0]
    },
    activePlayer: {
      type: Number,
      default: 0
    },
    isWiner: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    getNamePlayer(index) {
      let defaultName = 'Player ' + index
      // console.log(index, this.activePlayer, this.isWiner, defaultName)
      //nguoi hien tao, nguoi thang cuoc
      if(this.activePlayer == index && this.isWiner){
        defaultName = 'Winner!'
      }
      return defaultName
    }
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
  background-image: linear-gradient(
      rgba(62, 20, 20, 0.4),
      rgba(62, 20, 20, 0.4)
    ),
    url("../assets/back.jpg");
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
