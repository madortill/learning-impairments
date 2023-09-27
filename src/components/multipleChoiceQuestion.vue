<template>
  <div id="multiple-choice">
    <div class="content-container">
      <span class="question"> {{ question.question }} </span>
      <br> <span class="question"> בחרו את התשובה הנכונה! </span>
      <div class="answers">
        <ul class="list">
          <li v-for="(answer, index) in question.ans" :key="index" class="ans" @click="selectAnswer(index)">
            <img class="indication" :src="indicationScr(index)">
            <span>{{ answer }}</span>
          </li>
        </ul>
      </div>
      <button class="custom-btn btn-15 check" v-if="!showAnswers" @click="chosenAnswer !== -1 ? showAnswers = true : showEmpty = true">יאללה לבדוק!</button>
      <span v-if="showEmpty" class="error-message">אופס, נראה שלא ענית על השאלה</span>
      <button class="custom-btn btn-15 continue" v-show="showAnswers" @click="proceed">רוצה להמשיך</button>
    </div>
  </div>
</template>

<script>

  export default {
    name: "multiple-choice",
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
        this.$emit("finished");
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
      indicationScr(param) {
        let currSrc;
        if (this.showAnswers === false) {
          if (this.chosenAnswer === param) {
            currSrc = new URL("@/assets/images/blue-circle.svg", import.meta.url).href;
          } else {
            currSrc = new URL("@/assets/images/grey-circle.svg", import.meta.url).href;
          }
        } else {
          if (param === this.question.correct) {
            currSrc = new URL("@/assets/images/green-circle.svg", import.meta.url).href;
          } else if (this.chosenAnswer === param) {
            currSrc = new URL("@/assets/images/red-circle.svg", import.meta.url).href;
          } else {
            currSrc = new URL("@/assets/images/grey-circle.svg", import.meta.url).href;
          }
        }
        return currSrc;
      },
    }
  }
</script>

<style scoped>
  .content-container {
    position: absolute;
    height: 50vh;
    width: 55vw;
    background-color:rgba(255, 255, 255, 0.969);
    border-radius: 20px;
    text-align: center;
    top: -79vh;
    left: 24vw;
    font-size: 4vh;
  }
  
  .list {
    /* display: flex; */
  }

  li {
    /* text-align: right; */
    /* top: 20%; */
    left: 50%;
    /* position: absolute; */
    direction: rtl;
    display: flex;
    /* flex-direction: column; */
    /* transform: translate(50%); */
  }
  .indication {
    width: 1rem;
  }

  .ans {
    list-style: none;
    margin: 0.7rem;
  }

  .question,
  .ans {
    font-size: 1.5rem;
  }

  .ans:hover {
    cursor: pointer;
     
  }

  .answers {
    display: flex;
    justify-content: center;
  }

  .imgs {
    display: flex;
    list-style: none;
    margin-bottom: 1rem;
  }

  .check,
  .continue {
    border-radius: 3rem;
    border: 0.06rem solid rgb(255, 255, 255);
    width: fit-content;
    align-self: center;
    font-weight: 600;
    font-size: 0.9rem;
    background-color: rgb(0, 0, 0);
    color: white;
    position: relative;
    right: -1rem;
    margin: 1rem;
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

  button:hover {
    cursor: pointer;
  }


  .custom-btn {
  width: 130px;
  height: 40px;
  color: #000000;
  border-radius: 5px;
  padding: 10px 25px;
  font-family: 'Lato', sans-serif;
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

.btn-15 {
  background: #cecece;
  border: none;
  z-index: 1;
}
.btn-15:after {
  position: absolute;
  content: "";
  width: 0;
  height: 100%;
  top: 0;
  right: 0;
  z-index: -1;
  background-color: #4e4e4e;
  border-radius: 5px;
   box-shadow:inset 2px 2px 2px 0px rgba(255,255,255,.5),
   7px 7px 20px 0px rgba(0,0,0,.1),
   4px 4px 5px 0px rgba(0,0,0,.1);
  transition: all 0.3s ease;
}
.btn-15:hover {
  color: #fff;
}
.btn-15:hover:after {
  left: 0;
  width: 100%;
}
.btn-15:active {
  top: 2px;
}
</style>