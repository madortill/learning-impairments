<template>
    <div id="thirdBehavior">
      <div id="text" v-show="showText">
        <p style="text-align: center;">{{ myJson[22] }}</p>
        <div id="listsText">
          <p>{{ myJson[23] }}</p>
          <ul class="lists">
            <li v-for="(sentence, index) in myJson[24]" :key="index">
              <span>{{ sentence }}</span>
            </li>
          </ul>
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
  
  export default {
    name: "third-behavior",
    components: {},
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
        counter: 0,
        showOne: false
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
          setTimeout(() => {
            this.showQue = true;
            this.animations[3] = "fourtAnim";
            setTimeout(() => {
              this.inter = setInterval(() => {
                this.showPlus = !this.showPlus;
                this.counter++;
                if(this.counter === 5) {
                  clearInterval(this.inter);
                  this.showEight = false;
                  this.counter = 0;
                  this.inter = setInterval(() => {
                    this.showOne = !this.showOne;
                    this.counter++;
                    if(this.counter === 5) {
                      clearInterval(this.inter);
                      setTimeout(() => {
                        this.showAnim = false;
                        this.$emit("startZoomOut");
                        this.$emit("finishedLearning", 2);
                      }, 2000);
                    }
                  }, 500);
                }
              }, 500);
            }, 4000);
          }, 4500);
        }, 3000);
      },
  
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

#secNum {
  position: relative;
  top: 0vh;
  left: 0vh;
}

#thirdNum {
  visibility: visible;
}

#fourthNum {
  display: inline;
  top: 0vh;
}

#fifthNum {
  visibility: hidden;
}

.fifthAnim {
  animation: fifthAnim 4s forwards;
}

@keyframes fifthAnim {
  0% {
    visibility: hidden;
  }
  100% {
    visibility: visible;
  }
}

.fourtAnim {
  animation: fourtAnim 4s forwards;
}

@keyframes fourtAnim {
  0% {
    display: inline;
    top: 0vh;
  }
  100% {
    display: none;
    top: -2vh;
  }
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
    left: -6.3vh;
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
  background-repeat: no-repeat;
  background-size: 100vw 100vh;
  background-position: center;
  overflow: hidden;
  z-index: 0;
}

#numbers {
  position: absolute;
  z-index: 5;
  top: 30vh;
  left: 30vw;
  font-size: 4vh;
}

#text {
  height: 34vh;
  width: 39vw;
  position: absolute;
  top: 29vh;
  left: 32vw;
  text-align: right;
  font-size: 2.2vh;
}

#continueButton {
  position: absolute;
  top: 59vh;
  left: 33vw;
  font-family: buttons;
}

#listsText {
  position: relative;
  top: 0vh;
  right: 1vw;
}

#secList {
  position: relative;
  left: -23vw;
  top: -15vh;
}

.lists {
  position: relative;
  top: 0vh;
}

li {
  direction: rtl;
  text-align: right;
}
</style>