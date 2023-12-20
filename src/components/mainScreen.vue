<template>
    <div id="mainScreen" :class="zoomClassAnimation">
      <img id="teacher" src="../assets/images/teacher.svg" :class="zoomTeacherAnim">
      <div id="bubbleSpeech" v-show="showBubble && text === 1">
        <h3>!שלום לך<br> היום נלמד על לקויות למידה</h3>
        <button id="startButton" @click="showLearning" class="custom-btn btn-1">התחלנו</button>
    </div>
    
    <div class="learningText" v-if="showLearningText && learningText === 1" >
        <div class="containerText" >
          <div id="lineHead">מהי לקות למידה?</div>
          <div id="text1">{{(myJson[1])}}</div>
          <ul>
            <li v-for="(sent, index) in content" :key="index" v-show="currcontent === 2">
              <span>{{ sent }}</span>
            </li>
          </ul>
          <img src="../assets/images/next-arrow.png" class="nextArrow arrow" @click="nextText" v-show="showArrowLeft">
        </div>
    </div>

    <div id="text2" v-if="showLearningText && (learningText === 2 || learningText === 1)">
      <div class="conDiffrerent" >
        <div>
            <p style="font-size: 3vmin;" v-show="currcontent >= 3">{{(myJson[3])}}</p>
            <p id="different" class="firstScreenTwo" v-show="currcontent >= 4">{{(myJson[4])}}</p>
            <p id="different" class="firstScreenTwo" v-show="currcontent >= 5">{{(myJson[5])}}</p>
        </div>
        <div >
            <p style="font-size: 3vmin;" v-show="currcontent >= 6">{{(myJson[6])}}</p>
            <p id="different" class="secondScreenTwo" v-show="currcontent >= 7">{{(myJson[7])}}</p>
            <p id="different" class="secondScreenTwo" v-show="currcontent >= 8">{{(myJson[8])}}</p>
            <p id="different" class="secondScreenTwo" v-show="currcontent >= 9">{{(myJson[9])}}</p>
        </div>
      </div>
      <div class="conArrow">
        <img src="../assets/images/back-arrow.png" class="arrow" @click="backText" v-show="showArrowRigth">
        <p class="thirdScreenTwo" v-show="currcontent >= 10">{{(myJson[10])}}</p>
        <img src="../assets/images/next-arrow.png" class="arrow" @click="nextText" v-show="showArrowLeft">
      </div>
    </div>

    <questions @finishQuestion="showNext" :type="numQuestion" v-if="showQuestions"></questions>
    
    <div id="box">
    <student v-for="(percent, index) in grayscale" :finish="finishesStud" class="stud" ref="studs" :countGrey="percent" @changeGrey="showCurrentBehavior(index)" :studentNum="index" :key="index" v-if="showStudents"></student>
    <component :is="`behavior${currentStudent + 1}`" v-if="showBehavior" @finishedLearning="finished" @finish="finishedCurrLearning" @startZoom="zoomBg" @startZoomOut="zoomOutBg"></component>
    <div v-show="finishedLearn" id="finishText">
      <p>{{ myJson[27] }}</p>
      <p>{{ myJson[28] }}</p>
      <p>{{ myJson[29] }}</p>
      <button class="custom-btn btn-14" id="finishButton" @click="finishLomda">סיימתי את הלומדה!</button>
    </div>
    <div class="question-wrapper" :style="currentStudent !== 3 ? 'display: contents': ''">
      <questions @finishQuestion="showNextQuestion" :type="numQuestion" v-if="showQues && numQuestion === 4"></questions>
      <questions @finishQuestion="showNextQuestion" :type="numQuestion" v-if="showQues && numQuestion === 5"></questions>
      <questions @finishQuestion="showNextQuestion" :type="numQuestion" v-if="showQues && numQuestion === 11"></questions>
    </div>
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
        showLearning() {
          this.text = 0;
            this.showStudents = false;
            this.zoomClassAnimation = 'zoomClassAnim';
            this.zoomTeacherAnim = 'zoomTeacherAnim';
            setTimeout(() => {
                this.text = 2;
            }, 3500);
            setTimeout(() => {
              this.showLearningText = true;
              this.showBubble = false;
              this.currcontent++;
              this.showArrowLeft = true;
            }, 2500);
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
          console.log("gili");
          this.showLearningText = false;
          this.showArrowRigth = false;
          this.showArrowLeft = false;
          this.showQuestions = false;
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
}


#finishText {
  height: 34vh;
  width: 39vw;
  position: absolute;
  top: -29vh;
  left: 32vw;
  text-align: right;
  font-size: 2.2vmin;
  text-align: center;
  color: rgb(201, 201, 201);
}

#text2 {
  font-size: 2vmin;
  text-align: center;
  display: flex;
  direction: rtl;
  color: white;
  height: 90vh;
  width: 95vw;
  flex-direction: column;
  flex-wrap: nowrap;
  justify-content: center;
  align-items: center;
}

.thirdScreenTwo {
  width: 30vw;
  height: 10vh;
  font-size: 2.5vmin;
}

#different {
  height: 14vh;
  width: 9vw;
  float: right;
  background-color: black;
  border-radius: 1vh;
  margin-right: 1vw;
  font-size: 1.75vh;
}

.secondScreenTwo {
  right: 19vw;
  top: -14vh;
}

li {
  direction: rtl;
  text-align: right;
  font-size: 3.2vmin;
}

#lineHead {
  font-size: 4.5vmin;
  font-weight: bold;
  text-align: center;
}

#text1 {
  height: 10vh;
  width: 60vw;
  font-size: 3.2vmin;
  direction: rtl;
  text-align: center;
}

.learningText {
  color: white;
  height: 100vh;
  width: 95vw;
  display: flex;
  flex-direction: column;
  flex-wrap: nowrap;
  justify-content: center;
  align-items: center;
  direction: rtl;
    
}


#finishButton {
  position: absolute;
  top: 23vh;
  left: 0vw;
}
.arrow {
    height: 9vh;
    width: 4vw;
}

#projector:hover,
.arrow:hover {
  cursor: pointer;
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

#startButton {
    position: relative;
    left: 3.5vw;
    top: -0.1vh;
    width: 3vw;
    height: 2.2vh;
}

h3 {
    text-align: center;
    margin: 1vh;
}

#bubbleSpeech {
  background-image: url("@/assets/images/bubble.svg");
  background-size: 100% 100%;
  height: 16vh;
  width: 10vw;
  position: absolute;
  top: 37vh;
  left: 23.5vw;
}

#bubble1 {
  height: 15vh;
  width: 10vw;
  position: absolute;
  top: 0vh;
  left: 0vw;
}

#secBubbleSpeech {
  background-image: url("@/assets/images/bubble.svg");
  background-size: 100% 100%;
  height: 16vh;
  width: 10vw;
  position: absolute;
  top: 32vh;
  left: 17vw;
}

#teacher {
    height: 40vh;
    width: auto;
    position: absolute;
    top: 53vh;
    right: 78vw;
} 

#box {
    display: flex;
    justify-content: space-between;
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
  }
}

@keyframes zoomTeacher {
  0% {
    transform: scale(100%, 100%);
  }
  100% {
    transform: scale(170%, 170%) translate(-50%, 10%);
  }
}

.zoomOutClassAnim {
  animation: zoomOutClass 3s forwards;
}

@keyframes zoomOutClass {
  0% {
    background-size: 130vw 130vh;
  }
  100% {
   background-size: 100vw 100vh;
  }
}

.zoomOutTeacherAnim {
  animation: zoomOutTeacher 3s forwards;
}

@keyframes zoomOutTeacher {
  0% {
    right: 84vw;
    top: 49vh;
  }
  100% {
    right: 78vw;
    top: 53vh;
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

.question-wrapper {
  position: absolute !important;
  top: -52vh;
  left: 42vw;
}

.containerText {
  display: flex;
  height: 50vh;
  width: 70vw;
  flex-direction: column;
  flex-wrap: nowrap;
  justify-content: space-between;
  align-items: center;
}

.conDiffrerent {
  width: 65vw;
  height: 30vh;
  display: flex;
  flex-wrap: nowrap;
  justify-content: space-around;
}

.conArrow {
  width: 40vw;
  height: 15vh;
  display: flex;
  align-items: center;
}
</style>
  