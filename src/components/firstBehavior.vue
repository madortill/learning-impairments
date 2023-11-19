<template>
    <div id="firstBehavior">
      <img src="../assets/images/plane.png" v-show="showplane" class="plane" @click="showContent">
      <p id="helpText" v-show="showHelp">לחצו עליי</p>
      <div class="learning" v-if="showLearning">
        <div class="text1" v-show="text === 1">
          <p id="firstTitle">דיסלקציה</p>
          <p class="headText">{{ myJson[11] }}</p>
          <p class="centerText">{{ myJson[12] }}</p>
          <ul>
            <li v-for="(sentence, index) in myJson[13]" :key="index">
              <span>{{ sentence }}</span>
            </li>
          </ul>
          <p class="centerText">{{ myJson[14] }}</p>
          <ul>
            <li v-for="(sent, index) in myJson[15]" :key="index">
              <span>{{ sent }}</span>
            </li>
          </ul>
        </div>
        <img src="../assets/images/colors.jpg" id="colors" v-show="text === 2">
        <p id="nextButton" style="font-size: 2vmin; left: 3vw; top: 85vh;" v-show="text === 1" @click="nextLearning">להמשיך</p>
        <p id="nextButton" style="font-size: 2vmin; left: 3vw; top: 85vh;" v-show="text === 2" @click="nextLearning">סיימתי</p>
        <p id="beforeButton" style="font-size: 2vmin; left: 28vw; top: 85vh;" v-show="text === 2" @click="beforeLearning">הקודם</p>
      </div>
      <div v-if="showAnimation">
        <img src="../assets/images/eyes.svg" id="eyes">
        <div class="typewriter" @animationend="onAnimationEnd">
          <h1 v-if="type >= 0" style="top: -66vh;">{{ contant[0] }}</h1>
          <h1 v-if="type >= 1" style="top: -61vh;">{{ contant[1] }}</h1>
          <h1 v-if="type >= 2" style="top: -56vh;">{{ contant[2] }}</h1>
        </div>
        <p id="animButton" v-show="showButton" @click="closeAnimation">יאללה להמשיך</p> 
      </div>
      <questions @finishQuestion="showNextQuestion" :type="numQuestion" v-if="showQuestions && numQuestion === 2"></questions>
      <questions @finishQuestion="showNext" :type="numQuestion" v-if="showQuestions && numQuestion === 10"></questions>
    </div>
  </template>
     
  <script>
  import json from '@/data.json';
  import questions from '@/components/questions.vue'  
  
  export default {
    name: "first-behavior",
    components: {questions},
    data() {
      return {
        showLearning: false,
        showHelp: false,
        text: 1,
        showAnimation: false,
        contant: ["די---סקלצקיה:",
        "קו  שי ברח  איש   ט",
        "מומנ  וט  אכרי אה",],
        type: 0,
        showplane: true,
        showButton: false,
        myJson: json["content"][0],
        numQuestion: 2,
        showQuestions: false
      };
    },
    methods: {
      showContent() {
        this.showLearning = true;
        this.showHelp = false;
      },
      nextLearning() {
        if(this.text === 1){ 
          this.text = 2;
        } 
        else if(this.text === 2){ 
          this.showLearning = false;
          setTimeout(() => {
            this.showplane = false;
            this.showHelp = false;
            this.$emit("startZoom");
          }, 1000);
          setTimeout(() => {
            this.showAnimation = true;
          }, 3500);
        } 
      },
      beforeLearning() {
        if(this.text === 2){
          this.text = 1;
        } 
      },
      onAnimationEnd (event) {
        if (event.animationName.includes('typing')) {
          event.target.style.border = 'none';
          if (this.type < 4) {
            this.type++;
            if(this.type === 3) {
              this.showButton = true;
            }
          }
        }
      },
      closeAnimation() {
        this.showQuestions = true;
        this.showAnimation = false;
      },
      showNext() {
        this.numQuestion = 0;
        this.$emit("startZoomOut");
        this.$emit("finishedLearning", 0);
      },
      showNextQuestion() {
        this.numQuestion = 10;
      }
    },
    mounted() {
      setTimeout(() => {
        if(!this.showLearning && this.showplane) {
          this.showHelp = true;
        }
      }, 5000);
    }
  }
  
  
  </script>
    
<style scoped>
.learning {
    background-image: url("../assets/images/paper.svg");
    background-repeat: no-repeat;
    height: 93vh;
    width: 38vw;
    position: absolute;
    top: -74vh;
    right: 31vw;
    font-size: 2.5vmin;
    text-align: center;
}

#colors {
  height: 60vh;
  width: 30vw;
  position: relative;
  top: 17vh;
  right: 1.3vw;
}

#eyes {
  height: 100vh;
  width: 100vw;
  position: absolute;
  bottom: 3vh;
  left: 0;
}

#firstTitle {
  font-weight: bold;
  left: 3vw;
  position: relative;
  font-size: 3vmin;
}

.centerText {
  text-align: right;
}

.text1 {
  position: relative;
  top: 5vh;
  right: 5vw;
}

.headText {
  width: 25vw;
  position: relative;
  left: 10vw;
}

li {
  direction: rtl;
  text-align: right;
  margin-right: 2vw;
}

@font-face {
  font-family: buttons;
  src: url("../assets/fonts/miriwin-webfont.ttf");
}

#nextButton, #beforeButton {
  font-family: buttons;
}

#nextButton:hover, 
#beforeButton:hover,
#animButton:hover {
  cursor: pointer;
}

#animButton {
  font-family: buttons;
  position: absolute;
  top: -40vh;
  left: 27vw;
}

#nextButton { 
  position: absolute;
  left: 1vw;
  top: 82vh;
  height: 3vh;
  width: 5vw;
}

#beforeButton {
  position: absolute;
  left: 34vw;
  top: 82vh;
  height: 3vh;
  width: 5vw;
}

#helpText {
  position: absolute;
  top: 0vh;
  right: 67vw;
  font-size: small;
  color: white;
}

.plane:hover {
  cursor: pointer;
}
.plane {
  height: 16vh;
  width: 8vw;
  position: absolute;
  top: 26vh;
  right: 0vw;
  animation: plane 3s forwards;
}

@keyframes plane {
  0% {
    top: -35vh;
    right: -9vw;
}
100% {
    top: -3vh;
    right: 65vw;
}
}

.typewriter h1 {
  position: absolute;
  display: block;
  right: 34vw;
  top: -80vh;
  color: #000000;
  /* Ensures the content is not revealed until the animation */
  overflow: hidden;
  direction: rtl;
  /* The typwriter cursor */
  border-left: .15em solid rgb(0, 0, 0);
  /* Keeps the content on a single line */
  white-space: nowrap;
  letter-spacing: .15em;
  animation:
    typing 3.5s steps(30, end),
    blink-caret .5s step-end infinite;
}

/* The typing effect */
@keyframes typing {
  from {
    width: 0;
  }
  to {
    width: 34rem;
  }
}

/* The typewriter cursor effect */
@keyframes blink-caret {

  from,
  to {
    border-left-color: transparent;
  }

  50% {
    border-left-color: black;
  }
}

</style>
  