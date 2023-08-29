<template>
    <div id="multiple-choice-question">
      <div class="content-container">
        <span class="question"> {{ question.question }} </span>
        <br> <span class="question"> בחרו את התשובה הנכונה! </span>
        <div class="answers">
          <ul style="padding-right: 0; margin: 0; border-collapse: collapse;">
            <li v-for="(answer, index) in question.ans" :key="index" :class="[index === chosenAnswer ? 'selected' : '', 'ans']" @click="selectAnswer(index)">
              <img class="indication" v-show="showAnswers && (index === question.correct || index === chosenAnswer)" :src="indicationScr(index)">
              <span>{{ answer }}</span>
            </li>
          </ul>
        </div>
        <button v-if="!showAnswers" class="check" @click="chosenAnswer !== -1 ? showAnswers = true : showEmpty = true">בדוק אותי!</button>
        <span v-if="showEmpty" class="error-message">אופס, נראה שלא ענית על השאלה</span>
        <button class="continue" v-show="showAnswers" @click="proceed">בואו נמשיך</button>
      </div>
    </div>
  </template>
  
  <script>
  
    export default {
      name: "multiple-choice-question",
      props: ["question"],
      data() {
        return {
          chosenAnswer: -1,
          showAnswers: false,
          showEmpty: false
        }
      },
      methods: {
        proceed() {
          this.showAnswers = false;
          this.showEmpty = false;
          this.chosenAnswer =  -1;
          this.$emit('finished');
        },
        indicationScr(param) {
          if (param === this.ques.correct) {
            return new URL("@/assets/correct.svg", import.meta.url).href;
          } else {
            return new URL("@/assets/wrong.svg", import.meta.url).href;
          }
        },
        selectAnswer(num) {
          if (!this.showAnswers) {
            if (this.chosenAnswer !== num) {
              this.chosenAnswer = num;
              this.showEmpty = false;
            } else {
              this.chosenAnswer = -1;
            }
          }
        },
      }
    }
  </script>
  
  <style scoped>
    .content-container {
      width: 25rem; 
      height: 100%;
      background-image: url("@/assets/background-text.svg");
      background-repeat: no-repeat;
      background-size: cover;
      padding: 10%;
      display: flex;
      flex-direction: column;
    }
  
    .indication {
      width: 1rem;
    }
  
    .ans {
      list-style: none;
      margin: 0.7rem;
      border: 0.02rem solid black;
    }
  
    .question,
    .ans {
      font-size: 0.8rem;
    }
  
    .ans:hover {
      cursor: pointer;
       
    }
  
    .answers {
      display: flex;
      border-collapse: collapse;
    }
  
    .imgs {
      display: flex;
      list-style: none;
      margin-bottom: 1rem;
    }
  
    .selected {
      border: 0.1rem solid white;
    }
  
    .check,
    .continue {
      border-radius: 3rem;
      border: 0.06rem solid black;
      width: fit-content;
      align-self: center;
      font-weight: 500;
      font-size: 0.6rem;
      background-color: rgba(255, 255, 255, 0.5);
    }
  
    .check:hover,
    .continue:hover {
      cursor: pointer;
    }
  
    .error-message {
      font-size: 0.6rem;
      color: red;
      margin-right: 1rem;
    }
    
  </style>