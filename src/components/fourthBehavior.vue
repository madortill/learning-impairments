<template>
    <div id="fourthBehavior">
      <div id="whiteBg" v-show="showWhiteBg" @click="closeWhite"><p id="compText">לחצו עליי בשביל לעבור ללמוד על הלקות הבאה</p></div>
      <div id="blackBg" v-show="showBlackBg">
        <div id="google" v-show="showText">
          <h2 style="text-align: center;">הפרעות קשב וריכוז</h2>
          <p>{{(myJson[30])}}</p>    
          <p>{{(myJson[31])}}</p>
          <p>{{(myJson[32])}}</p>
          <p>{{(myJson[33])}}</p>
          <ul>
            <li v-for="(sentence, index) in (myJson[34])" :key="index">
              <span>{{ sentence }}</span>
            </li>
          </ul>
          <p>{{(myJson[35])}}</p>
          <ul>
            <li v-for="(sent, index) in (myJson[36])" :key="index">
              <span>{{ sent }}</span>
            </li>
          </ul>
        </div>
        <!-- <button id="continueButton" @click="closeText" v-show="showText">להמשיך</button> -->
        <button class="custom-btn btn-2" id="continueButton" @click="closeText" v-show="showText">להמשיך</button>
      </div>
      <questions @finishQuestion="showNext" :type="numQuestion" v-if="showQues && numQuestion === 6"></questions>
    </div>
  </template>
     
  <script>
  import json from '@/data.json';
  import questions from '@/components/questions.vue'
  
  export default {
    name: "fourth-behavior",
    components: {questions},
    data() {
      return {
        showWhiteBg: true,
        nIntervId: '',
        showBlackBg: false,
        myJson: json["content"][0],
        showQues: false,
        numQuestion: 6,
        showText: false
      };
    },
    methods: {
      changeBg() {
        this.showWhiteBg = !this.showWhiteBg;
      },
      closeWhite() {
        clearInterval(this.nIntervId);
        this.showWhiteBg = false;
        this.showBlackBg = true;
        this.showText = true;
      },
      closeText() {
        this.showText = false;
        this.showQues = true;
      },
      showNext() {
        this.numQuestion = 0;
        this.showBlackBg = false;
        this.$emit("finish");
        this.$emit("finishedLearning", 3);
      },
    },
    // mounted() {
    //   this.nIntervId = setInterval(this.changeBg, 1500);
    // }
  }
  
  
  </script>
    
<style scoped>
#whiteBg {
  background-color: rgba(250, 250, 250, 0.493);
  height: 13.4vh;
  width: 10.5vw;
  position: absolute;
  top: -50.5vh;
  left: 14.3vw;
  z-index: 9;
  display: block;
}

#whiteBg:hover {
  cursor: pointer;
}

#compText {
  text-align: center;
  font-size: x-large;
}

#blackBg {
  background-color: rgba(0, 0, 0, 0.5);
  height: 101vh;
  width: 100vw;
  top: -75vh;
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
  direction: rtl;
  font-size: 2vmin;
}

#continueButton {
  position: absolute;
  top: 84vh;
  left: 31vw;
  background-color: rgb(209, 209, 209);
}

.btn-2 {
  background: rgb(96,9,240);
  background: linear-gradient(0deg, rgba(96,9,240,1) 0%, rgba(129,5,240,1) 100%);
  border: none;
}
.btn-2:before {
  height: 0%;
  width: 2px;
}
.btn-2:hover {
  box-shadow:  4px 4px 6px 0 rgba(255,255,255,.5),
              -4px -4px 6px 0 rgba(116, 125, 136, .5), 
    inset -4px -4px 6px 0 rgba(255,255,255,.2),
    inset 4px 4px 6px 0 rgba(0, 0, 0, .4);
}

.custom-btn {
  width: 5vw;
  height: 4vh;
  border-radius: 5px;
  padding: 10px 25px;
  font-family: 'Lato', sans-serif;
  font-weight: 500;
  background: transparent;
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
  display: inline-block;
   box-shadow:inset 2px 2px 2px 0px rgba(255,255,255,.5),
   7px 7px 20px 0px rgba(0,0,0,.1),
   4px 4px 5px 0px rgba(0,0,0,.1);
  outline: none;
}

#questions {
  position: absolute;
  top: 24vh;
}
</style>