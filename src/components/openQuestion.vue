<template>
    <div id="openQuestion">
      <div id="question">
        <p>{{ question.question }}</p>
        <input type="text" id="answer" v-model="inputValue">
        <button id="checkButton" @click="checkAnswer">בדיקה</button> 
        <br><br>
        <span v-if="!showAnswer && checked" class="emptyMsg">אופס, נראה שלא ענית על השאלה</span>
        <div v-show="showAnswer">תשובה נכונה: {{ question.correct }}</div>
        <button id="closeBtn" @click="finish" v-show="showEndBtn">סיימתי</button>
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
  background-color:aqua;
  text-align: center;
  top: -30vh;
  left: -20vw;
  font-size: 4vh;
}

#closeBtn {
  position: absolute;
  height: 4vh;
  width: 4vw;
  top: 40vh;
  right: 49vw;
}

#question {
  position: relative;
  top: 3vh;
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
</style>
  