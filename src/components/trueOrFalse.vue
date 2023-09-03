<template>
    <div id="trueOrFalse">
      <div id="question">
        <p>{{ question.question }}</p>
        <button id="trueBtn" @click="checkAnswerTrue">נכון </button>
        <button id="falseBtn" @click.once="checkAnswerFalse">לא נכון </button>
        <br><br>
        <span v-show="showCorrect === 1" class="correct">מצוין! תשובה נכונה</span>
        <span v-show="showCorrect === 2" class="incorrect">אופס, תשובה שגויה! נסה שוב</span>
        <button id="closeBtn" @click="finish">סיימתי</button>
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
        answer: true,
        showCorrect: 0
      };
    },
    methods: {
        checkAnswerTrue() {
            this.answer ? this.showCorrect = 1 : this.showCorrect = 2;
        },
        checkAnswerFalse() {
            !this.answer ? this.showCorrect = 1 : this.showCorrect = 2;
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
#trueOrFalse {
    position: relative;
    height: 50vh;
    width: 55vw;
    background-color:aqua;
    text-align: center;
    top: -25vh;
    left: -15vw;
    font-size: 4vh;
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
</style>
  