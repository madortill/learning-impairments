<template>
    <div id="openScreen">
      <div id="background"></div>
      <p>ברוכים הבאים ללומדת לקויות למידה!</p>
      <button class="custom-btn btn-12"><span @click="showAnim">#התחלנו</span><span>באלי להתחיל</span></button>
      <!-- <div><vue-iframe v-if="startAnim" id="animate" src="/animations/startAnim/startAnim.html" /></div> -->
    </div>
  </template>
     
  <script>
  
  
  export default {
    name: "open-screen",
    components: {},
    data() {
      return {
        startAnim: false,
      };
    },
    methods: {
        showAnim() {
            this.startAnim = true;
            setTimeout(() => {
                this.startAnim = false;
                this.$emit("done");
            }, 3000);
        }
    },
  }
  
  
  </script>
    
<style scoped>
#open-screen {
    overflow: hidden;
}

#background {
    background-image: url("../assets/images/bgOpenScreen.jpg");
    background-repeat: no-repeat;
    background-size: 100vw 100vh;
    height: 100vh;
    width: 100vw;
}

p {
    font-size: 5vh;
    text-align: center;
    position: absolute;
    top: 40vh;
    right: 35vw;
}

.custom-btn {
  width: 6.770833333333333vw;
  height: 4.12796697626419vh;
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
  box-shadow: inset 2px 2px 2px 0px rgba(255, 255, 255, .5),
    7px 7px 20px 0px rgba(0, 0, 0, .1),
    4px 4px 5px 0px rgba(0, 0, 0, .1);
  outline: none;
}

.btn-12 {
  position: relative;
  left: 40vw;
  bottom: 30vh;
  border: none;
  box-shadow: none;
  width: 180px;
  height: 90px;
  line-height: 42px;
  -webkit-perspective: 230px;
  perspective: 230px;
}

.btn-12 span {
  background: rgb(32, 56, 100);
  background: linear-gradient(0deg, rgb(32, 56, 100) 0%, rgb(32, 56, 100) 100%);
  display: block;
  position: absolute;
  width: 130px;
  height: 40px;
  box-shadow: inset 2px 2px 2px 0px rgba(255, 255, 255, .5),
    7px 7px 20px 0px rgba(0, 0, 0, .1),
    4px 4px 5px 0px rgba(0, 0, 0, .1);
  border-radius: 5px;
  margin: 0;
  text-align: center;
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
  -webkit-transition: all .3s;
  transition: all .3s;
}

.btn-12 span:nth-child(1) {
  box-shadow:
    -7px -7px 20px 0px #fff9,
    -4px -4px 5px 0px #fff9,
    7px 7px 20px 0px #0002,
    4px 4px 5px 0px #0001;
  -webkit-transform: rotateX(90deg);
  -moz-transform: rotateX(90deg);
  transform: rotateX(90deg);
  -webkit-transform-origin: 50% 50% -20px;
  -moz-transform-origin: 50% 50% -20px;
  transform-origin: 50% 50% -20px;
}

.btn-12 span:nth-child(2) {
  -webkit-transform: rotateX(0deg);
  -moz-transform: rotateX(0deg);
  transform: rotateX(0deg);
  -webkit-transform-origin: 50% 50% -20px;
  -moz-transform-origin: 50% 50% -20px;
  transform-origin: 50% 50% -20px;
}

.btn-12:hover span:nth-child(1) {
  box-shadow: inset 2px 2px 2px 0px rgba(255, 255, 255, .5),
    7px 7px 20px 0px rgba(0, 0, 0, .1),
    4px 4px 5px 0px rgba(0, 0, 0, .1);
  -webkit-transform: rotateX(0deg);
  -moz-transform: rotateX(0deg);
  transform: rotateX(0deg);
}

.btn-12:hover span:nth-child(2) {
  box-shadow: inset 2px 2px 2px 0px rgba(255, 255, 255, .5),
    7px 7px 20px 0px rgba(0, 0, 0, .1),
    4px 4px 5px 0px rgba(0, 0, 0, .1);
  color: transparent;
  -webkit-transform: rotateX(-90deg);
  -moz-transform: rotateX(-90deg);
  transform: rotateX(-90deg);
}
</style>
  