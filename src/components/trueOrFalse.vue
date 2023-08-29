<template>
    <div id="trueOrFalse">
      <p>{{ question.question }}</p>
      <button id="trueBtn" @click.once="checkAnswerTrue">נכון </button>
      <button id="falseBtn" @click.once="checkAnswerFalse">לא נכון </button>
      <br><br>
      <span v-show="showCorrect === 1" class="correct">מצוין! תשובה נכונה</span>
      <span v-show="showCorrect === 2" class="incorrect">אופס, תשובה שגויה! נסה שוב</span>
    </div>
  </template>
     
  <script>
  
  
  export default {
    name: "true-or-false",
    components: {},
    props: ["question"],
    data() {
      return {
        answer: question.correct,
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
        }
    },
    mounted() {
      
    }
  }
  
  
  </script>
    
<style scoped>
#trueOrFalse {
    position: absolute;
    height: 20vh;
    width: 20vw;
    background-color:aqua;
    text-align: center;
    top: 35vh;
    left: 40vw;
}
.correct {
    color: rgb(56, 156, 101);
}
.incorrect {
    color: rgb(199, 52, 52);
}

#trueBtn {
   margin: 1vw;
   height: 3vh;
   width: 3vw;
}

#falseBtn {
    height: 3vh;
    width: 3vw;
}
</style>
  