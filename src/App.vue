<template>
  <div id="app">
    <div class="wrapper clearfix">
      <Players
        v-bind:scorePlayer = "scorePlayer"
        v-bind:activePlayer = "activePlayer"
        v-bind:currentScore = "currentScore"
        v-bind:isWiner = "isWiner"
      />
      <Controls
        v-on:handleNewGame = "handleNewGame"
        v-on:handleRoleDice = "handleRoleDice"
        v-on:handleHoldScore = "handleHoldScore"
        v-bind:finalScore = "finalScore"
        v-on:handleChangeFinalScore = "handleChangeFinalScore"
        v-bind:isPlay = "isPlay"
      />
      <Dices
        v-bind:dices = "dices"
      />
      <PopupRule
        v-on:handleConfirm = "handleConfirm"
        v-bind:isOpenPopup = "isOpenPopup"
      />
    </div>
  </div>
</template>
<script>
import Players from '@/components/Players'
import Controls from '@/components/Controls'
import Dices from '@/components/Dices'
import PopupRule from '@/components/PopupRule'
export default {
  name: "App",
  data() {
      return {
          isPlay: false,
          isOpenPopup: false,
          currentScore: 100,
          activePlayer: 1,
          dices: [ 3, 5 ],
          scorePlayer: [ 0, 0 ],
          finalScore: 10
      }
  },
  components: {
    Players,
    Controls,
    Dices,
    PopupRule
  },
  computed: {
    isWiner() {
      let { scorePlayer, finalScore } = this
      if(scorePlayer[0] >= finalScore || scorePlayer[1] >= finalScore){
        //dung cuoc cho
        this.isPlay = false
        return true
      } else {
        return false
      }
    }
  },
  methods: {
    handleChangeFinalScore(e) {
      let number = parseInt(e.target.value)
      if(isNaN(number)){
        this.finalScore = ''
      } else {
        console.log(number)
        this.finalScore = number
      }
    },
    handleHoldScore() {
      if(this.isPlay){
        console.log('handleHoldScore')
        let{ scorePlayer, activePlayer, currentScore} = this
        let scoreOld = scorePlayer[activePlayer-1]
        this.$set(this.scorePlayer, activePlayer-1, scoreOld + currentScore)
        if(!this.isWiner) {
          this.nextPlayer()
        }
        // this.scorePlayer[activePlayer-1] =scoreOld + currentScore
        // this.scorePlayer[this.activePlayer-1] = this.scorePlayer[this.activePlayer-1] + this.currentScore
        // console.log(scorePlayer[this.activePlayer-1])
      } else {
        alert("vui long nhan vao nut newgame")
      }
    },
    nextPlayer() {
      this.activePlayer = this.activePlayer == 1 ? 2 : 1
      this.currentScore = 0
    },
    handleConfirm() {
      console.log('handleconfirm app vue')
      this.isOpenPopup = false
      this.isPlay = true
      this.currentScore = 0
      this.activePlayer = 1
      this.scorePlayer = [ 0, 0 ]
      this.dices = [ 1, 1 ]
    },
    handleNewGame() {
      console.log('newgame app vue')
      //hien thi popup->show luat choi
      this.isOpenPopup = true
    },
    handleRoleDice() {
      console.log('handleRoleDice in app vue')
      if(this.isPlay == true) {
        //se xoay xuc xac
        let dice1 = Math.floor(Math.random()*6) + 1
        let dice2 = Math.floor(Math.random()*6) + 1
        console.log(dice1, dice2)
        this.dices = [ dice1, dice2 ]
        if(dice1 ===1 || dice2 == 1){
          //doii luot choi
          //reset diem
          setTimeout(() => { //de xu ly bat dong bo
            alert('Player ' + this.activePlayer+ ' da quay vao o mat luot!')
            this.nextPlayer()
          }, 10);
        } else {
          //cong don diemm
          this.currentScore = this.currentScore +dice1 + dice2
        }
      } else {
        alert("vui long nhan vao nut newgame")
      }
    }
  }
}
</script>
<style>

</style>
