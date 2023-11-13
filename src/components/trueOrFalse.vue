<template>
    <div id="trueOrFalse">
      <div id="question">
        <p>{{ question.question }}</p>
        <button id="trueBtn" class="button-4" @click="checkAnswerTrue">נכון </button>
        <button id="falseBtn" class="button-4" @click="checkAnswerFalse">לא נכון </button>
        <br><br>
        <span v-show="showCorrect === 'correct'" class="correct">מצוין! תשובה נכונה</span>
        <span v-show="showCorrect === 'incorrect'" class="incorrect">אופס, תשובה שגויה! נסה שוב</span>
        <button id="closeBtn" class="button-4" @click="finish" v-if="this.showCorrect === 'correct' ">סיימתי</button>
      </div>
    </div>
  </template>
     
  <script>
  
  
  export default {
    name: "true-or-false",
    components: {},
    props: ["question"],
    data() {
      return {
        answer: this.question.correct,
        showCorrect: '',
        clicked: false
      };
    },
    methods: {
        checkAnswerTrue() {
          this.answer ? this.showCorrect = 'correct' : this.showCorrect = 'incorrect';
        },
        checkAnswerFalse() {
          !this.answer ? this.showCorrect = 'correct' : this.showCorrect = 'incorrect';
        },
        finish() {
          this.$emit("finished");
        }
    },
  }
  
  
  </script>
    
<style scoped>
#trueOrFalse {
    position: relative;
    height: 50vh;
    width: 55vw;
    background-color:rgba(255, 255, 255, 0.969);
    border-radius: 20px;
    text-align: center;
    top: -25vh;
    left: -15vw;
    font-size: 4vh;
    color: black;
}

#question{
  position: relative;
  top: 4vh;
}
.correct {
    color: rgb(56, 156, 101);
}
.incorrect {
    color: rgb(199, 52, 52);
}

#trueBtn {
   margin: 1vw;
   height: 6vh;
   width: 6vw;
   font-size: 2vh;
}

#falseBtn {
    height: 6vh;
    width: 6vw;
    font-size: 2vh;
}

#closeBtn {
  position: absolute;
  height: 4vh;
  width: 4vw;
  top: 40vh;
  right: 49vw;
}

.button-4 {
  appearance: none;
  background-color: #bad6dd;
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
  