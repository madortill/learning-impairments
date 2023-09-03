<template>
    <div id="mainScreen" :class="zoomClassAnimation">
      <div id="teacher" :class="zoomTeacherAnim"></div>
      <div id="bubbleSpeech" v-show="showBubble && text === 1">
        <h3>!שלום לך</h3>
        <h3>היום נלמד על לקויות למידה</h3>
        <button id="startButton" @click="closeStartText">התחלנו</button> 
    </div>
    <div id="secBubbleSpeech" v-show="showBubble && text === 2">
        <h3>!ועכשיו, לחצו על המקרן וחשפו את החומר</h3>
        <div id="projector" @click="showLearning"></div>
    </div>
    <div id="learningText" v-show="showLearningText">
        <div v-show="learningText === 1">
          <p id="lineHead">מהי לקות למידה?</p>
          <br>
          <p id="text1">{{(myJson[1])}}</p>
          <ul style="position: relative; left: 2vw;">
            <li v-for="(sent, index) in content" :key="index" v-show="currcontent === 2">
              <span>{{ sent }}</span>
            </li>
          </ul>
        </div>
        <div id="text2" v-show="learningText === 2">
          <p style="font-size: 3vh; top: -4vh; position: relative; right: -1vw;" v-show="currcontent >= 3">{{(myJson[3])}}</p>
          <p id="different" class="firstScreenTwo" v-show="currcontent >= 4">{{(myJson[4])}}</p>
          <p id="different" class="firstScreenTwo" v-show="currcontent >= 5">{{(myJson[5])}}</p>
          <p style="font-size: 3vh; top: -10.5vh; position: relative; right: 17vw;" v-show="currcontent >= 6">{{(myJson[6])}}</p>
          <p id="different" class="secondScreenTwo" v-show="currcontent >= 7">{{(myJson[7])}}</p>
          <p id="different" class="secondScreenTwo" v-show="currcontent >= 8">{{(myJson[8])}}</p>
          <p id="different" class="secondScreenTwo" v-show="currcontent >= 9">{{(myJson[9])}}</p>
          <p class="thirdScreenTwo" v-show="currcontent >= 10">{{(myJson[10])}}</p>
        </div>
        <img src="../assets/images/back-arrow.png" class="backArrow arrow" @click="backText" v-show="showArrowRigth">
        <img src="../assets/images/next-arrow.png" class="nextArrow arrow" @click="nextText" v-show="showArrowLeft">
        <questions @finishQuestion="showNext" :type="numQuestion" v-if="showQuestions"></questions>
    </div>
    
    <div id="box">
    <student v-for="(percent, index) in grayscale" :finish="finishesStud" class="stud" ref="studs" :countGrey="percent" @changeGrey="showCurrentBehavior(index)" :key="index" v-if="showStudents"></student>
    <component :is="`behavior${currentStudent + 1}`" v-if="showBehavior" @finishedLearning="finished" @finish="finishedCurrLearning" @startZoom="zoomBg" @startZoomOut="zoomOutBg"></component>
    <div v-show="finishedLearn" id="finishText">
      <p>{{ myJson[27] }}</p>
      <p>{{ myJson[28] }}</p>
      <p>{{ myJson[29] }}</p>
      <button class="custom-btn btn-14" id="finishButton" @click="finishLomda">סיימתי את הלומדה!</button>
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
        numQuestion: 1
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
                }, 1000);
            } 
            else if(this.learningText === 2){ 
                this.learningText = 1;
                console.log(this.currcontent);
                this.showQuestions = true;
                // this.showLearningText = false;
                // this.showArrowRigth = false;
                // this.showArrowLeft = false;
                // this.zoomClassAnimation = 'zoomOutClassAnim';
                // this.zoomTeacherAnim = 'zoomOutTeacherAnim';
                // setTimeout(() => {
                //     this.showStudents = true;
                //     this.finishesStud = true;
                // }, 3200);
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
          }, 3200);

        },
        showCurrentBehavior(number) {
          this.finishedLearn = false;
          this.currentStudent = number;
          console.log(number);
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
          this.$emit("done");
        }
    },
    mounted() {
      // console.log(this.content);
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
    background-image: url("../assets/images/classroom.jpg");
    background-repeat: no-repeat;
    background-size: 100vw 100vh;
    background-position: center;
    height: 100vh;
    width: 100vw;
}

#finishText {
  height: 34vh;
  width: 39vw;
  position: absolute;
  top: 30vh;
  left: 32vw;
  text-align: right;
  font-size: 2.2vh;
  text-align: center;
}

#text2 {
  font-size: 2vh;
  text-align: center;
}

.thirdScreenTwo {
  position: absolute;
  width: 30vw;
  height: 2vh;
  right: 28vw;
  top: 18vh;
  font-size: 2.5vh;
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

li {
  direction: rtl;
  text-align: right;
  position: relative;
  right: 30vw;
  font-size: 3vh;
}

#lineHead {
  font-size: 4.5vh;
  font-weight: bold;
  position: absolute;
  text-align: center;
  left: 5vw;
  margin: 0;
  top: -5vh;
}

#text1 {
  height: 10vh;
  width: 40vw;
  font-size: 3.2vh;
  text-align: center;
  position: relative;
  left: -8vw;
  top: -2vh;
}

#learningText {
    position: absolute;
    height: 38vh;
    width: 54vw;
    top: 26vh;
    left: 40vw;
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
    top: -25vh;
    left: 12vw;
}

.stud:hover {
  cursor: pointer;
}

#startButton {
    position: relative;
    left: 3.5vw;
    top: 1vh;
}

h3 {
    text-align: center;
    margin: 1vh;
}

#bubbleSpeech {
    background-color: rgb(247, 247, 247);
    height: 16vh;
    width: 10vw;
    position: absolute;
    top: 27vh;
    left: 23.5vw;
}

#secBubbleSpeech {
    background-color: rgb(247, 247, 247);
    height: 16vh;
    width: 10vw;
    position: absolute;
    top: 32vh;
    left: 17vw;
}

#teacher {
    background-color: black;
    height: 40vh;
    width: 7vw;
    position: absolute;
    right: 78vw;
    top: 40vh;
} 

#box {
    display: flex;
    justify-content: flex-start;
    height: 100%;
    width: 100%;
    flex-wrap: wrap;
    align-content: flex-end;
    align-items: flex-start;
    flex-direction: row-reverse;
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
    background-size: 130vw 130vh;
  }
}

@keyframes zoomTeacher {
  0% {
    right: 78vw;
    top: 40vh;
  }
  100% {
    right: 84vw;
    top: 49vh;
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
</style>
  