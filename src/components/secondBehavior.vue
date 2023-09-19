<template>
    <div id="secondBehavior">
      <div id="text" v-show="showText === 0">
        <p id="head">דיסגרפיה</p>
        <p style="text-align: center; position: relative; top: -2.5vh;">{{ myJson[16] }} {{ myJson[17] }}</p>
        <div id="listsText">
          <p>{{ myJson[18] }}</p>
          <ul class="lists">
            <li v-for="(sentence, index) in myJson[19]" :key="index">
              <span>{{ sentence }}</span>
            </li>
        </ul>
        <div id="secList">
          <p>{{ myJson[20] }}</p>
          <ul class="lists">
              <li v-for="(sent, index) in myJson[21]" :key="index">
                <span>{{ sent }}</span>
              </li>
          </ul>
        </div>
      </div>
    </div>
      <p id="continueButton" @click="closeStartText" v-show="showText === 0">רוצה להמשיך</p>
      <div id="notebook" v-show="showText === 1">
        <img src="../assets/images/hand.gif" id="animation" v-if="showAnim">
        <div id="canvas" v-if="showCanvas">
          <canvas id="myCanvas" width="540" height="290" @mousedown="beginDrawing" @mousemove="keepDrawing" @mouseup="stopDrawing"></canvas>
          <p id="instru">ועכשיו עברו על הטקסט עם היד החלשה שלכם</p>
          <p id="textCanvas">דיסגרפיה</p>
        </div>
        <button class="custom-btn btn-5" id="canvasButton" v-show="showButton" @click="closeCanvas"><span>יאללה להמשיך</span></button>
      </div>
    </div>
  </template>
     
  <script>
  import json from '@/data.json';
  
  export default {
    name: "second-behavior",
    components: {},
    data() {
      return {
        showText: 0,
        showAnim: false,
        showCanvas: true,
        x: 0,
        y: 0,
        isDrawing: false,
        canvas: null,
        showButton: false,
        myJson: json["content"][0],
      };
    },
    methods: {
      closeStartText() {
        this.showText = 1;
        this.showCanvas = true;
        setTimeout(() => {
          this.showButton = true;
        }, 5000);
      },
      closeCanvas() {
        this.showCanvas = false;
        this.showButton = false;
        this.showAnim = true;
        setTimeout(() => {
          this.showAnim = false;
          this.showText = 2;
          this.$emit("finishedLearning", 1);
        }, 6000);
      },
      drawLine(x1, y1, x2, y2) {
        let ctx = this.canvas;
        ctx.beginPath();
        ctx.strokeStyle = 'black';
        ctx.lineWidth = 4;
        ctx.moveTo(x1, y1);
        ctx.lineTo(x2, y2);
        ctx.stroke();
        ctx.closePath();
      },
      beginDrawing(e) {
        this.x = e.offsetX;
        this.y = e.offsetY;
        this.isDrawing = true;
      },
      keepDrawing(e) {
        if (this.isDrawing === true) {
          this.drawLine(this.x, this.y, e.offsetX, e.offsetY);
          this.x = e.offsetX;
          this.y = e.offsetY;
        }
      },
      stopDrawing(e) {
        if (this.isDrawing === true) {
          this.drawLine(this.x, this.y, e.offsetX, e.offsetY);
          this.x = 0;
          this.y = 0;
          this.isDrawing = false;
        }
      }
    },
    mounted() {
      var c = document.getElementById("myCanvas");
      this.canvas = c.getContext('2d');
    }
  }
  
  
  </script>
    
<style scoped>
@font-face {
  font-family: buttons;
  src: url("../assets/fonts/miriwin-webfont.ttf");
}

#animation {
  height: 30vh;
  width: 27vw;
  position: relative;
  z-index: 6;
  top: 34vh;
  left: 18vw;
}

#head {
  position: relative;
  font-weight: bold;
  text-align: center;
  font-size: 3vmin;
}

#whiteScreen {
  background-color: white;
  opacity: 0.5;
  height: 100%;
  width: 100%;
  z-index: -1;
  position: absolute;
}

#text {
  height: 34vh;
  width: 39vw;
  position: absolute;
  top: 24vh;
  left: 32vw;
  text-align: right;
  font-size: 2.2vmin;

}

#listsText {
  position: relative;
  top: -2vh;
  right: 1vw;
}

#secList {
  position: relative;
  left: -25vw;
  top: -15.5vh;
}

.lists {
  position: relative;
  top: -2vh;
}

li {
  direction: rtl;
  text-align: right;
}

#canvasButton {
  position: absolute;
  top: 66vh;
  left: 28vw;
}

#instru {
  position: absolute;
  top: 28.5vh;
  left: 26vw;
  font-size: 2.2vmin;
  font-family: canvas;
  font-weight: bold;
}

@font-face {
  font-family: canvas;
  src: url("../assets/fonts/dana.otf");
}

#textCanvas {
  position: relative;
  top: 24vh;
  left: 20vw;
  font-family: canvas;
  font-size: 14vmin;
  z-index: -1;
}

#myCanvas {
  border: 1px solid grey;
  background-color: rgb(255, 255, 255);
  border-radius: 2vh;
  position: absolute;
  top: 34vh;
  left: 16.5vw;
  opacity: 0.8;
}

#continueButton {
  position: absolute;
  top: 59vh;
  left: 32vw;
  font-family: buttons;
}

#continueButton:hover {
  cursor: pointer;
}

#notebook {
 position: relative;
  height: 100vh;
  width: 100vw;
  z-index: 1;
  overflow: hidden;
  background-image: url("../assets/images/notebook.svg");
  background-repeat: no-repeat;
  background-size: 100vw 100vh;
  z-index: 3;
}

.book-bg {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  z-index: -1;
}

.custom-btn {
  width: 4vw;
  height: 2vh;
  color: #fff;
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

/* 5 */
.btn-5 {
  width: 6vw;
  height: 4vh;
  line-height: 42px;
  padding: 0;
  border: none;
  background: rgb(0, 0, 0);
background: linear-gradient(0deg, rgb(0, 0, 0) 0%, rgb(0, 0, 0) 100%);
}
.btn-5:hover {
  color: #5cc2f1;
  background: transparent;
   box-shadow:none;
}
.btn-5:before,
.btn-5:after{
  content:'';
  position:absolute;
  top:0;
  right:0;
  height:2px;
  width:0;
  background: #5cc2f1;
  box-shadow:
   -1px -1px 5px 0px #fff,
   7px 7px 20px 0px #0003,
   4px 4px 5px 0px #0002;
  transition:400ms ease all;
}
.btn-5:after{
  right:inherit;
  top:inherit;
  left:0;
  bottom:0;
}
.btn-5:hover:before,
.btn-5:hover:after{
  width:100%;
  transition:800ms ease all;
}
</style>