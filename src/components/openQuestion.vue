<template>
    <div id="openQuestion">
      <div id="question">
        <p class="specificQuestion">{{ question.question }}</p>
        <input type="text" id="answer" v-model="inputValue">
        <button class="button-4" role="button" id="checkButton" @click="checkAnswer">בדיקה</button>
        <br><br>
        <span v-if="!showAnswer && checked" class="emptyMsg">אופס, נראה שלא ענית על השאלה</span>
        <div v-show="showAnswer">התשובה הנכונה: {{ question.correct }}</div>
        <button class="button-4" role="button" id="closeBtn" @click="finish" v-show="showEndBtn">סיימתי</button>
      </div>
    </div>
  </template>
     
  <script>
  
  
  export default {
    name: "open-question",
    components: {},
    props: ['question'],
    data() {
      return {
        showAnswer: false,
        inputValue: '',
        checked: false,
        showEndBtn: false
      };
    },
    methods: {
      checkAnswer() {
          this.checked = true;
          if(this.inputValue !== '') {
              this.showAnswer = true;
              this.showEndBtn = true;
          }
          else {
              this.showAnswer = false;
          }
      },
      finish() {
        this.$emit("finished");
      }
    },
    mounted() {
      
    }
  }
  
  
  </script>
    
<style scoped>
#openQuestion {
  position: relative;
  height: 50vh;
  width: 55vw;
  background-color:rgba(255, 255, 255, 0.969);
  border-radius: 20px;
  text-align: center;
  top: -30vh;
  left: -20vw;
  font-size: 4vh;
}

#closeBtn {
  position: absolute;
  height: 4vh;
  width: 4vw;
  top: 38vh;
  right: 49vw;
  text-align: center;
}

#question {
  position: relative;
  top: 3vh;
}

.specificQuestion {
  direction: rtl;
}


#answer {
  height: 5vh;
  width: 15vw;
}

#checkButton {
  height: 5.5vh;
  width: 5vw;
  font-size: 2vh;
  position: relative;
  left: 1vw;
}

.button-4 {
  appearance: none;
  background-color:#bad6dd;
  border: 1px solid rgba(27, 31, 35, 0.15);
  border-radius: 6px;
  box-shadow: rgba(27, 31, 35, 0.04) 0 1px 0, rgba(255, 255, 255, 0.25) 0 1px 0 inset;
  box-sizing: border-box;
  color: #24292E;
  cursor: pointer;
  display: inline-block;
  font-size: 14px;
  font-weight: 500;
  line-height: 20px;
  padding: 6px 16px;
  position: relative;
  transition: background-color 0.2s cubic-bezier(0.3, 0, 0.5, 1);
  user-select: none;
  -webkit-user-select: none;
  vertical-align: middle;
  white-space: nowrap;
  word-wrap: break-word;
}

.button-4:hover {
  background-color: #F3F4F6;
  text-decoration: none;
  transition-duration: 0.1s;
}

.button-4:disabled {
  background-color: #FAFBFC;
  border-color: rgba(27, 31, 35, 0.15);
  color: #959DA5;
  cursor: default;
}

.button-4:active {
  background-color: #EDEFF2;
  box-shadow: rgba(225, 228, 232, 0.2) 0 1px 0 inset;
  transition: none 0s;
}

.button-4:focus {
  outline: 1px transparent;
}

.button-4:before {
  display: none;
}

.button-4:-webkit-details-marker {
  display: none;
}
</style>
  