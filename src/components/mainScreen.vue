<template>
    <div id="mainScreen" :class="zoomClassAnimation">
      <img id="teacher" :class="zoomTeacherAnim" src="../assets/images/teacher.svg" />
      <div id="bubbleSpeech" v-show="showBubble && text === 1">
        <h3>שלום לך! <br> היום נלמד על לקויות למידה</h3>
        <button id="startButton" @click="closeStartText" class="custom-btn btn-1">התחלנו</button>
    </div>
    <div id="secBubbleSpeech" v-show="showBubble && text === 2">
        <h3>!ועכשיו, לחצו על המקרן וחשפו את החומר</h3>
        <div id="projector" @click="showLearning">CLICK ME</div>
    </div>
    <div id="learningText" v-show="showLearningText">
        <div v-show="learningText === 1">
          <p id="lineHead">מהי לקות למידה?</p>
          <br>
          <p id="text1">{{(myJson[1])}}</p>
          <ul>
            <li v-for="(sent, index) in content" :key="index" v-show="currcontent === 2">
              <span>{{ sent }}</span>
            </li>
          </ul>
        </div>
        <div id="text2" :style="learningText === 2? 'visibility: visible': 'visibility: hidden'">
          <p style="font-size: 3vmin; top: -4vh; position: relative; right: -1vw;" v-show="currcontent >= 3">{{(myJson[3])}}</p>
          <p id="different" class="firstScreenTwo" v-show="currcontent >= 4">{{(myJson[4])}}</p>
          <p id="different" class="firstScreenTwo" v-show="currcontent >= 5">{{(myJson[5])}}</p>
          <p style="font-size: 3vmin; top: -10.5vh; position: relative; right: 17vw;" v-show="currcontent >= 6">{{(myJson[6])}}</p>
          <p id="different" class="secondScreenTwo" v-show="currcontent >= 7">{{(myJson[7])}}</p>
          <p id="different" class="secondScreenTwo" v-show="currcontent >= 8">{{(myJson[8])}}</p>
          <p id="different" class="secondScreenTwo" v-show="currcontent >= 9">{{(myJson[9])}}</p>
          <p class="thirdScreenTwo" v-show="currcontent >= 10">{{(myJson[10])}}</p>
        </div>
        <img src="../assets/images/back-arrow.svg" class="backArrow arrow" @click="backText" v-show="showArrowRigth">
        <img src="../assets/images/next-arrow.svg" class="nextArrow arrow" @click="nextText" v-show="showArrowLeft">
        <questions @finishQuestion="showNext" :type="numQuestion" v-if="showQuestions"></questions>
    </div>
    
    <div id="box">
    <student v-for="(percent, index) in grayscale" :finish="finishesStud" class="stud" ref="studs" :countGrey="percent" @changeGrey="showCurrentBehavior(index)" :studentNum="index" :key="index" v-if="showStudents"></student>
    <component :is="`behavior${currentStudent + 1}`" v-if="showBehavior" @finishedLearning="finished" @finish="finishedCurrLearning" @startZoom="zoomBg" @startZoomOut="zoomOutBg"></component>
    <div v-show="finishedLearn" id="finishText">
      <p>{{ myJson[27] }}</p>
      <p>{{ myJson[28] }}</p>
      <p>{{ myJson[29] }}</p>
      <button class="custom-btn btn-14" id="finishButton" @click="finishLomda">סיימתי את הלומדה!</button>
    </div>
    <questions @finishQuestion="showNextQuestion" :type="numQuestion" v-if="showQues && numQuestion === 4"></questions>
    <questions @finishQuestion="showNextQuestion" :type="numQuestion" v-if="showQues && numQuestion === 5"></questions>
    <questions @finishQuestion="showNextQuestion" :type="numQuestion" v-if="showQues && numQuestion === 11"></questions>

  </div>
      
    </div>
  </template>
     
  <script>
  import student from '@/components/student.vue'
  import behavior1 from '@/components/firstBehavior.vue'
  import behavior2 from '@/components/secondBehavior.vue'
  import behavior3 from '@/components/thirdBehavior.vue'
  import behavior4 from '@/components/fourthBehavior.vue'  
  import dragQuestion from '@/components/dragQuestion.vue'  
  import openQuestion from '@/components/openQuestion.vue'  
  import multipleChoiceQuestion from '@/components/multipleChoiceQuestion.vue'  
  import trueOrFalse from '@/components/trueOrFalse.vue'  
  import questions from '@/components/questions.vue'  
  import json from '@/data.json';
  
  export default {
    name: "main-screen",
    components: {student, behavior1, behavior2, behavior3, behavior4, dragQuestion, openQuestion, multipleChoiceQuestion, trueOrFalse, questions},
    data() {
      return {
        grayscale: [0, 0.9, 0.9, 0.9],
        text: 1,
        showStudents: true,
        zoomClassAnimation: '',
        showLearningText: false,
        learningText: 1,
        showBubble: true,
        countGrey: 0.9,
        // When currentStudent is -1, no behavior component is shown
        currentStudent: -1,
        finishesStud: false,
        showBehavior: false,
        currentBehavior: '',
        zoomTeacherAnim: '',
        finishedLearn: false,
        firstTime: true,
        currQuest: 1,
        currcontent: 1,
        myJson: json["content"][0],
        arrText1: (json["questions"][0][this.currQuestion]),
        showArrowRigth: false,
        showArrowLeft: false,
        interval: '',
        classCursos: '',
        showQuestions: false,
        numQuestion: 1,
        arrNumQuestion: [4, 5, 11],
        counterQuestions: 0,
        showQues: false
      };
    },
    methods: {
        closeStartText() {
            this.text = 0;
            this.showStudents = false;
            this.zoomClassAnimation = 'zoomClassAnim';
            this.zoomTeacherAnim = 'zoomTeacherAnim';
            setTimeout(() => {
                this.text = 2;
            }, 3500);
        },
        showLearning() {
            this.showLearningText = true;
            this.showBubble = false;
            setTimeout(() => {
              this.currcontent++;
              this.showArrowLeft = true;
            }, 2000);
        },
        backText() {
            if(this.learningText === 2){
                this.learningText = 1;
                this.currcontent--;
                this.showArrowRigth = false;
            } 
        },
        nextText() {
            if(this.learningText === 1) { 
                this.learningText = 2;
                this.showArrowLeft = false;
                this.interval = setInterval(() => {
                  this.currcontent++;
                  if(this.currcontent === 10) {
                    this.showArrowRigth = true;
                    this.showArrowLeft = true;
                    clearInterval(this.interval);
                  }
                }, 1500);
            } 
            else if(this.learningText === 2){ 
                this.learningText = 1;
                this.showQuestions = true;
            } 
        },
        showNext() {
          this.showLearningText = false;
          this.showArrowRigth = false;
          this.showArrowLeft = false;
          this.zoomClassAnimation = 'zoomOutClassAnim';
          this.zoomTeacherAnim = 'zoomOutTeacherAnim';
          setTimeout(() => {
              this.showStudents = true;
              this.finishesStud = true;
              this.numQuestion = 4;
              this.counterQuestions++;
          }, 3200);

        },
        showCurrentBehavior(number) {
          this.finishedLearn = false;
          this.currentStudent = number;
          if (number !== (this.grayscale.length - 1) && this.firstTime) {
            this.showBehavior = true;
          }
          this.firstTime = false;
        },
        zoomBg() {
            this.showStudents = false;
            this.zoomClassAnimation = 'zoomClassAnim';
            this.zoomTeacherAnim = 'zoomTeacherAnim';
        },
        zoomOutBg() {
            this.zoomClassAnimation = 'zoomOutClassAnim';
            this.zoomTeacherAnim = 'zoomOutTeacherAnim';
            setTimeout(() => {
                this.showStudents = true;
            }, 3000);
        },
        finishedCurrLearning() {
          this.finishedLearn = true;
        },
        finished(number) {
          this.currentStudent = number;
          this.firstTime = false;
          if (number !== (this.grayscale.length - 1)) {
            this.grayscale[number + 1] = 0;
            this.showBehavior = true;
          }
        },
        finishLomda() {
          this.finishedLearn = false;
          this.showQues = true;
          this.showStudents = false;
        },
        showNextQuestion() {
          if(this.counterQuestions === 1) {
            this.counterQuestions++;
            this.numQuestion++;
          }
          else if(this.counterQuestions === 2) {
            this.counterQuestions++;
            this.numQuestion = 11;
          } 
          else if(this.counterQuestions === 3) {
            this.$emit("done");
          }
        }
    },
    mounted() {
    },
    computed: {
      content() {
        return (json["content"][0][2]);
      }
    }
  }
  
  
  </script>
    
<style scoped>
#mainScreen {
    background-image: url("../assets/images/classroom.svg");
    background-repeat: no-repeat;
    background-size: 100vw 100vh;
    background-position: 50% 80%;
    height: 100vh;
    width: 100vw;
    --teacher-left-offset: 15vw;
}

#finishText {
  height: 34vh;
  width: 39vw;
  position: absolute;
  top: 30vh;
  left: 32vw;
  text-align: right;
  font-size: 2.2vmin;
  text-align: center;
}

.thirdScreenTwo {
  position: absolute;
  width: 30vw;
  height: 2vh;
  right: 28vw;
  top: 18vh;
  font-size: 2.5vmin;
}

#different {
  height: 13vh;
  width: 9vw;
  float: right;
  position: relative;
  background-color: aliceblue;
  border-radius: 1vh;
  margin-right: 1vw;
}

.firstScreenTwo {
  right: 15vw;
  top: -8vh;
}

.secondScreenTwo {
  right: 19vw;
  top: -14vh;
}

/* Text on board */
#learningText {
  position: absolute;
  top: 47%;
  left: 45.5%;
  direction: rtl;
  text-align: right;
  transform: translate(-50%, -50%);
  width: 69vw;
  /* background-color: maroon; */
  font-size: 3vmin;
  padding: 1% 2%;
  box-sizing: border-box;
  color: rgb(225, 225, 224);
}

#lineHead {
  font-size: 4.5vmin;
  font-weight: bold;
  text-align: center;
  margin: 0;
}

#text1 {
  font-size: 3.2vmin;
  margin-bottom: 2%;
  margin-top: 0;
}

#text2 {
  font-size: 2vmin;
  text-align: center;
}



#finishButton {
  position: absolute;
  top: 30vh;
  left: 0vw;
}
.arrow {
    height: 9vh;
    width: 4vw;
    position: absolute;
    top: 32vh;
}

#projector:hover,
.arrow:hover {
  cursor: pointer;
}

.backArrow {
    right: 17vw;
}

.nextArrow {
    right: 64vw;
}

#projector {
    position: absolute;
    height: 6vh;
    width: 44vw;
    top: -10vh;
    left: 8vw;
    background-color: aliceblue;
}

.stud:hover {
  cursor: pointer;
}


h3 {
    text-align: center;
    margin: 1vh;
}

#bubbleSpeech {
  direction: rtl;
  background-image: url("@/assets/images/bubble.svg");
  background-size: 100% 100%;
  height: 16vh;
  width: 7vw;
  position: absolute;
  bottom: 45vh;
  left: calc(var(--teacher-left-offset) + 8vw);
  padding: 0.2% 2%;

}

#startButton {
    right: 50%;
    width: 4vw;
    height: 2.5vh;
}

#teacher {
    /* background-color: black; */
    height: 42vh;
    width: auto;
    position: absolute;
    left: var(--teacher-left-offset);
    bottom: 5vh;
} 

#bubble1 {
  height: 15vh;
  width: 10vw;
  position: absolute;
  top: 0vh;
  left: 0vw;
}

#secBubbleSpeech {
    /* background-color: rgb(247, 247, 247); */
  background-image: url("@/assets/images/bubble.svg");
  background-size: 100% 100%;
  height: 16vh;
  width: 10vw;
  position: absolute;
  top: 32vh;
  left: 17vw;
}


#box {
    display: flex;
    justify-content: space-between;
    /* height: 100%; */
    width: 100%;
    flex-wrap: wrap;
    align-content: flex-end;
    flex-direction: row-reverse;
    position: absolute;
    bottom: -3vh;
}
.zoomClassAnim {
  animation: zoomClass 3s forwards;
}
.zoomTeacherAnim {
  animation: zoomTeacher 3s forwards;
}

@keyframes zoomClass {
  0% {
    background-size: 100vw 100vh;
  }
  100% {
    background-size: 170vw 170vh;
    /* background-position: 50% 80%; */
  }
}

@keyframes zoomTeacher {
  0% {
    transform: scale(100%, 100%) translateX();
  }
  100% {
    transform: scale(170%, 170%) translateX(-70%);
  }
}

.zoomOutClassAnim {
  animation: zoomClass 3s reverse;
}

.zoomOutTeacherAnim {
  animation: zoomTeacher 3s reverse;
}

@keyframes zoomOutTeacher {
  0% {
    right: 84vw;
    top: 49vh;
  }
  100% {
    right: 78vw;
    top: 40vh;
  }
}

.custom-btn {
  width: 6vw;
  height: 3.5vh;
  color: #fff;
  border-radius: 5px;
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
/* 14 */
.btn-14 {
  background: #22c1c9;
  border: none;
  z-index: 1;
}
.btn-14:after {
  position: absolute;
  content: "";
  width: 100%;
  height: 0;
  top: 0;
  left: 0;
  z-index: -1;
  border-radius: 5px;
  background-color: #a6f1f5;
  background-image: linear-gradient(315deg, #a6f1f5 0%, #a6f1f5 74%);
   box-shadow:inset 2px 2px 2px 0px rgba(255,255,255,.5),
   7px 7px 20px 0px rgba(0,0,0,.1),
   4px 4px 5px 0px rgba(0,0,0,.1);
  transition: all 0.3s ease;
}
.btn-14:hover {
  color: #000;
}
.btn-14:hover:after {
  top: auto;
  bottom: 0;
  height: 100%;
}
.btn-14:active {
  top: 2px;
}

student:hover {
  cursor: pointer;
}

.btn-1 {
  background: rgb(170, 170, 170);
  background: linear-gradient(0deg, rgb(170, 170, 170) 0%, rgb(170, 170, 170) 100%);
  border: none;
}
.btn-1:hover {
   background: rgb(192, 191, 191);
background: linear-gradient(0deg, rgb(192, 191, 191) 0%, rgb(192, 191, 191) 100%);
}
</style>
  