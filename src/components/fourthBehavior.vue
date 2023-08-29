<template>
    <div id="fourthBehavior">
      <div id="whiteBg" v-show="showWhiteBg" @click="closeWhite"><p id="compText">לחצו עליי בשביל לעבור ללמוד על הלקות הבאה</p></div>
      <div id="blackBg" v-show="showBlackBg">
        <div id="google">text</div>
        <button id="continueButton" @click="closeText">להמשיך</button>
      </div>
    </div>
  </template>
     
  <script>
  
  
  export default {
    name: "fourth-behavior",
    components: {},
    data() {
      return {
        showWhiteBg: true,
        nIntervId: '',
        showBlackBg: false
      };
    },
    methods: {
      changeBg() {
        this.showWhiteBg = !this.showWhiteBg;
        console.log(this.showWhiteBg);
      },
      closeWhite() {
        clearInterval(this.nIntervId);
        this.showWhiteBg = false;
        this.showBlackBg = true;
      },
      closeText() {
        this.showBlackBg = false;
        this.$emit("finish");
        this.$emit("finishedLearning", 3);
      }
    },
    mounted() {
      this.nIntervId = setInterval(this.changeBg, 1500);
    }
  }
  
  
  </script>
    
<style scoped>
#whiteBg {
  background-color: rgba(250, 250, 250, 0.493);
  height: 13.4vh;
  width: 10.5vw;
  position: absolute;
  top: 21.5vh;
  left: 14.3vw;
}

#compText {
  text-align: center;
  font-size: x-large;
}

#blackBg {
  background-color: rgba(0, 0, 0, 0.5);
  height: 100%;
  width: 100%;
  top: 0;
  left: 0;
  position: absolute;
}

#google {
  height: 80vh;
  width: 40vw;
  position: absolute;
  top: 10vh;
  left: 30vw;
  background-color: white;
}

#continueButton {
  position: absolute;
  top: 85vh;
  left: 32vw;
}
</style>