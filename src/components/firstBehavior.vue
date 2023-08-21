<template>
    <div id="firstBehavior">
      <img src="../assets/images/plain.png" class="plain" @click="showContent">
      <p id="helpText" v-show="showHelp">לחצו עליי</p>
      <div class="learning" v-if="showLearning">
        <p v-show="text === 1">text</p>
        <p v-show="text === 2">color exercise</p>
        <p id="nextButton" v-show="text === 1" @click="nextLearning">להמשיך</p>
        <p id="nextButton" v-show="text === 2" @click="nextLearning">סיימתי</p>
        <p id="beforeButton" v-show="text === 2" @click="beforeLearning">הקודם</p>
      </div>
      <div v-if="showAnimation">
        <div class="typewriter">
          <h1 v-if="type >= 0" style="top: 15vh;">{{ contant[0] }}</h1>
          <h1 v-if="type >= 1" style="top: 20vh;">{{ contant[1] }}</h1>
          <h1 v-if="type >= 2" style="top: 25vh;">{{ contant[2] }}</h1>
          <h1 v-if="type >= 3" style="top: 30vh;">{{ contant[3] }}</h1>
        </div>
      </div>
    </div>
  </template>
     
  <script>
  
  
  export default {
    name: "first-behavior",
    components: {},
    data() {
      return {
        showLearning: false,
        showHelp: false,
        text: 1,
        showAnimation: false,
        contant: ["אנימציה של הקלדה של משפטים שהוא",
        "קורא מהלוח ובהקלדה יראו איך הוא",
        "בעצם קורא (מלא שגיאות, קטיעות",
        "וסימני שאלה)"],
        type: 0,
      };
    },
    methods: {
      showContent() {
        this.showLearning = true;
        this.showHelp = false;
      },
      nextLearning() {
        if(this.text === 1){ 
          this.text = 2;
        } 
        else if(this.text === 2){ 
          this.showLearning = false;
          this.showHelp = false;
          setTimeout(() => {
            this.$emit("startZoom");
          }, 1000);
          setTimeout(() => {
            this.typeNext();
          }, 3500);
        } 
      },
      beforeLearning() {
        if(this.text === 2){
          this.text = 1;
        } 
      },
      typeNext() {
        this.showAnimation = true;
        console.log("hhh");
        setTimeout(() => {
          if (this.type < 4) {
            this.type++;
            this.typeNext();
          } 
        }, 2000);
      }
    },
    mounted() {
      setTimeout(() => {
        if(!this.showLearning) {
          this.showHelp = true;
        }
      }, 5000);
    }
  }
  
  
  </script>
    
<style scoped>
.learning {
    background-image: url("../assets/images/paper.jpg");
    background-repeat: no-repeat;
    height: 87vh;
    width: 37vw;
    position: absolute;
    top: 7vh;
    right: 33vw;
}

#nextButton { 
  position: absolute;
  left: 1vw;
  top: 82vh;
  height: 3vh;
  width: 5vw;
}

#beforeButton {
  position: absolute;
  left: 34vw;
  top: 82vh;
  height: 3vh;
  width: 5vw;
}

#helpText {
  position: absolute;
  top: 56.7vh;
  right: 73vw;
  font-size: small;
}
.plain {
  height: 16vh;
  width: 8vw;
  position: absolute;
  top: 26vh;
  right: 0vw;
  animation: plain 3s forwards;
}

@keyframes plain {
  0% {
    top: 26vh;
    right: 0vw;
  }
  100% {
    top: 50vh;
    right: 71vw;
  }
}

.typewriter h1 {
  position: absolute;
  display: block;
  right: 15vw;
  color: #000000;
  font-family: monospace;
  overflow: hidden;
  width: 30rem;
  border: black solid 2px;
  /* Ensures the content is not revealed until the animation */
  border-right: .15em solid rgb(0, 0, 0);
  /* The typwriter cursor */
  white-space: nowrap;
  /* Keeps the content on a single line */
  /* margin: 0 auto; */
  /* Gives that scrolling effect as the typing happens */
  letter-spacing: .15em;
  /* Adjust as needed */
  animation:
    typing 3.5s steps(30, end),
    blink-caret .5s step-end infinite;
}

/* The typing effect */
@keyframes typing {
  from {
    width: 0
  }
  to {
    width: 100%
  }
}

/* The typewriter cursor effect */
@keyframes blink-caret {

  from,
  to {
    border-color: transparent
  }

  50% {
    border-color: rgba(255, 166, 0, 0)
  }
}


/* Hadar's code */
/* Animation */
.anim-typewriter {
  animation: typewriter 3.2s steps(44) normal both,
  blinkTextCursor 500ms steps(44) 7 both;
}

.anim-typewriter-short {
  animation: typewriterShort 1.5s steps(20) normal both,
  blinkTextCursor 500ms steps(20) 2 both;
}

@keyframes typewriter{
  from{width: 0;}
  to{width: 18em;}
}

@keyframes typewriterShort{
  from{width: 0;}
  to{width: 9em;}
}

@keyframes blinkTextCursor{
  from{border-left-color: rgba(255,255,255,.75);}
  to{border-left-color: transparent;}
}

</style>
  