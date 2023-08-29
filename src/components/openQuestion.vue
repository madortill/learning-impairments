<template>
    <div id="openQuestion">
        <p>{{ question.question }}</p>
        <input type="text" id="answer" v-model="inputValue">
        <button id="checkButton" @click="checkAnswer">בדיקה</button> 
        <br><br>
        <span v-if="!showAnswer && checked" class="emptyMsg">אופס, נראה שלא ענית על השאלה</span>
        <div v-show="showAnswer">תשובה נכונה: {{ question.correct }}</div>
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
        checked: false
      };
    },
    methods: {
        checkAnswer() {
            this.checked = true;
            if(this.inputValue !== '') {
                this.showAnswer = true;
            }
            else {
                this.showAnswer = false;
            }
        }
    },
    mounted() {
      
    }
  }
  
  
  </script>
    
<style scoped>
#openQuestion {
    background-color: aqua;
    height: 34vh;
    width: 39vw;
    position: absolute;
    top: 29vh;
    left: 32vw;
    text-align: center;
}

#question {
    position: absolute;
    top: 10vh;
}

.emptyMsg {

}
</style>
  