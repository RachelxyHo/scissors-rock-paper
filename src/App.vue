<template>
  <div id="container">
    <div id="bot-placeholder">
      <img :src="bot_image">
    </div>
    <div id="you-placeholder">
      <img :src="you_image">
    </div>
    <div id="buttons-container">
      <div v-on:click="chooseItem(1)" id="btn-paper"></div>
      <div v-on:click="chooseItem(2)" id="btn-scissor"></div>
      <div v-on:click="chooseItem(3)" id="btn-rock"></div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'app',
  data() {
    return {
      botChoice: 0,
      userChoice: 0,
    }
  },
  methods: {
    chooseItem: function (index) {
      this.userChoice = index;
      this.botChoice = Math.floor(Math.random()*3) + 1;
      if(this.userChoice==this.botChoice){
        this.userChoice += 100;
        this.botChoice += 100;
      }else if (this.userChoice==1&&this.botChoice==2){
        this.userChoice = 20;
        this.botChoice = -10;
      }else if (this.userChoice==2&&this.botChoice==1){
        this.userChoice = -10;
        this.botChoice = 20;
      }else if (this.userChoice==2&&this.botChoice==3){
        this.userChoice = -20;
        this.botChoice = 30;
      }else if (this.userChoice==3&&this.botChoice==2){
        this.userChoice = 30;
        this.botChoice = -20;
      }else if (this.userChoice==1&&this.botChoice==3){
        this.userChoice = 10;
        this.botChoice = -30;
      }else if (this.userChoice==3&&this.botChoice==1){
        this.userChoice = -30;
        this.botChoice = 10;
      }
    

    }

  },
  computed: {
    bot_image() {
      let botChoices = {};
      botChoices['-30'] = 'rock-lose.png';
      botChoices['-20'] = 'scissor-lose.png';
      botChoices['-10'] = 'paper-lose.png';
      botChoices['0'] = 'Placeholder-Bot.png';
      botChoices['10'] = 'paper-win.png';
      botChoices['20'] = 'scissor-win.png';
      botChoices['30'] = 'rock-win.png';
      botChoices['101'] = 'paper-draw.png';
      botChoices['102'] = 'scissor-draw.png';
      botChoices['103'] = 'rock-draw.png';

      return `/images/${botChoices[this.botChoice]}`
    },
    you_image() {
      let userChoices = {};
      userChoices['-30'] = 'rock-lose.png';
      userChoices['-20'] = 'scissor-lose.png';
      userChoices['-10'] = 'paper-lose.png';
      userChoices['0'] = 'Placeholder-You.png';
      userChoices['10'] = 'paper-win.png';
      userChoices['20'] = 'scissor-win.png';
      userChoices['30'] = 'rock-win.png';
      userChoices['101'] = 'paper-draw.png';
      userChoices['102'] = 'scissor-draw.png';
      userChoices['103'] = 'rock-draw.png';

      return `/images/${userChoices[this.userChoice]}`
    },
      
  },
  
}
</script>
 
<style>
#container {
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 100vh;
  padding-top: 40px;
  box-sizing: border-box;
  background-color: #44D7B6;
}
 
#bot-placeholder, #you-placeholder {
  flex: 0px 2 1;
}
 
#bot-placeholder img, #you-placeholder img {
  display: block;
  width: 60%;
  height: auto;
  margin: auto;
}
 
#buttons-container {
  flex: 0px 1 1;
  display: flex;
  flex-direction: row;
}
 
#buttons-container div {
  flex: 0px 1 1;
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center bottom;
}
 
#buttons-container div#btn-paper {
  background-image: url('/public/images/paper-btn.png');
}
 
#buttons-container div#btn-scissor {
  background-image: url('/public/images/scissor-btn.png');
}
 
#buttons-container div#btn-rock {
  background-image: url('/public/images/rock-btn.png');
}
</style>