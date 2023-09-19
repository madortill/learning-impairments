<template>
    <div id="thirdBehavior">
      <div id="text" v-show="showText">
        <p id="head">דיסקלקוליה</p>
        <p style="text-align: center; position: relative; top: -2.5vh;">{{ myJson[22] }}</p>
        <div id="listsText">
          <div id="firstList">
            <p>{{ myJson[23] }}</p>
            <ul class="lists">         
              <li v-for="(sentence, index) in myJson[24]" :key="index">
                <span>{{ sentence }}</span>
              </li>
            </ul>
          </div>
          <div id="secList">
            <p>{{ myJson[25] }}</p>
            <ul class="lists">
                <li v-for="(sent, index) in myJson[26]" :key="index">
                  <span>{{ sent }}</span>
                </li>
            </ul>
          </div>
        </div>
      </div>
      <p id="continueButton" @click="closeStartText" v-show="showText">רוצה להמשיך</p>
      <questions @finishQuestion="showNextQuestion" :type="numQuestion" v-if="showQues && numQuestion === 3"></questions>
      <questions @finishQuestion="showNext" :type="numQuestion" v-if="showQues && numQuestion === 7"></questions>
      <div id="animations" v-if="showAnim">
        <img src="../assets/images/eyes.svg" id="eyes">
        <div id="numbers">
          <p id="firstExer"> 
            <span>3</span>
            <span :class="animations[0]" id="firstNum">7 </span>
            <span>+ </span>
            <span :class="animations[1]" id="secNum">7</span>
            <span :class="animations[2]" id="thirdNum">5 </span>
            <span>= </span>
            <span v-if="showQue">?</span>
            <span v-if="showQue">? </span>
          </p>
          <p id="secExer"> 
            <span>1</span>
            <span>7 </span>
            <span v-show="!showPlus">- </span>
            <span v-show="showPlus">+ </span>
            <span v-show="showEight">8 </span>
            <span>= </span>
            <span v-show="!showEight">8 </span>
          </p>
          <p id="thirdExer"> 
            <span>1</span>
            <span v-if="!showOne">6 </span>
            <span v-if="showOne">1 </span>
            <span>* </span>
            <span>1</span>
            <span>1 </span>
            <span>= </span>
            <span v-if="showOne">1111 </span>
          </p>
        </div>
      </div>
    </div>
  </template>
     
  <script>
  import json from '@/data.json';
  import questions from '@/components/questions.vue'  
  
  export default {
    name: "third-behavior",
    components: {questions},
    data() {
      return {
        showText: true,
        showAnim: false,
        myJson: json["content"][0],
        animations: ["", "", "", ""],
        showQue: false,
        showPlus: false,
        showEight: true,
        inter: '',
        inter2: '',
        counter: 0,
        counter2: 0,
        showOne: false,
        showQues: false,
        numQuestion: 3,
      };
    },
    methods: {
      closeStartText() {
        this.showText = false;
        this.$emit("startZoom");
        setTimeout(() => {
          this.showAnim = true;
          this.animations[0] = "firstAnim";
          this.animations[1] = "secAnim";
          this.animations[2] = "thirdAnim";
          this.showQue = true;
          this.inter = setInterval(() => {
            this.showPlus = !this.showPlus;
            this.counter++;
            if(this.counter === 7) {
              clearInterval(this.inter);
              this.showEight = false;
            }
          }, 500);
          this.inter2 = setInterval(() => {
            this.showOne = !this.showOne;
            this.counter2++;
            if(this.counter2 === 7) {
              clearInterval(this.inter2);
              setTimeout(() => { 
                this.showAnim = false;
                this.showQues = true;
                // this.$emit("startZoomOut");
                // this.$emit("finishedLearning", 2);
              }, 3000);
            }
          }, 500);
        }, 3000);
      },
      showNext() {
        this.numQuestion = 0;
        this.$emit("startZoomOut");
        this.$emit("finishedLearning", 2);
      },
      showNextQuestion() {
        this.numQuestion = 7;
      }
  
    },
    mounted() {
      
    }
  }
  
  
  </script>
    
<style scoped>
@font-face {
  font-family: buttons;
  src: url("../assets/fonts/miriwin-webfont.ttf");
}

#firstNum {
  position: relative;
  top: 0vh;
  left: 0vh;
}

#head {
  position: relative;
  font-weight: bold;
  text-align: center;
  font-size: 3vmin;
}

#secNum {
  position: relative;
  top: 0vh;
  left: 0vh;
}

#thirdNum {
  visibility: visible;
}

.firstAnim {
  animation: firstAnim 4s forwards;
}

@keyframes firstAnim {
  0% {
    top: 0vh;
    left: 0vh;
  }
  50% {
    top: -4vh;
    left: 3.3vh;
  }
  100% {
    top: 0vh;
    left: 0vh;
  }
}

.secAnim {
  animation: secAnim 4s forwards;
}

@keyframes secAnim {
  0% {
    top: 0vh;
    left: 0vh;
  }
  50% {
    top: -4vh;
    left: -3vh;
  }
  100% {
    top: 0vh;
    left: -5.5vh;
  }
}

.thirdAnim {
  animation: thirdAnim 4s forwards;
}

@keyframes thirdAnim {
  0% {
    visibility: visible;
  }
  100% {
    visibility: hidden;
  }
}

#firstExer,
#secExer ,
#thirdExer {
  position: relative;
}

#firstExer {
  left: 5vw;
}

#secExer {
  left: 28vw;
  top: -8vh;
}

#thirdExer {
  left: 15vw;
}

#eyes {
  height: 100vh;
  width: 100vw;
  position: absolute;
  bottom: 0;
  left: 0;
}

#numbers {
  position: absolute;
  z-index: 5;
  top: 30vh;
  left: 30vw;
  font-size: 4vmin;
}

#text {
  height: 34vh;
  width: 39vw;
  position: absolute;
  top: 25vh;
  left: 32vw;
  text-align: right;
  font-size: 2.2vmin;
}

#continueButton {
  position: absolute;
  top: 59vh;
  left: 33vw;
  font-family: buttons;
}

#continueButton:hover {
  cursor: pointer;
}

#listsText {
  position: relative;
  top: -1vh;
  right: 1vw;
}

#firstList {
  position: relative;
  right: 2vw;
  top: -1.5vh;
}
#secList {
  position: relative;
  left: -21vw;
  top: -17vh;
}

.lists {
  position: relative;
  top: -2vh;
}

li {
  direction: rtl;
  text-align: right;
}
</style>