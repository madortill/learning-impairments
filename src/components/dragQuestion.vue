<template>
    <div id="dragQuestion">
        <div id="first" v-show="showFirst">
            <div id="firstQuestion">לקות למידה</div>
            <div id="secondQuestion">קושי למידה</div>
            <div id="draggable-container">
                <div class="" draggable="true" @dragstart="onDragging" id="1">
                    <p id="text1">נובעת מגורם פנימי, מולדת, קבועה</p>
                </div>
            </div>

            <div id="draggable-container2">
                <div class="" draggable="true" @dragstart="onDragging" id="2">
                    <p id="text2">נובע מגורם חיצוני, נרכש, זמני</p>
                </div>
            </div>

            <div id="box-droppable1" @drop="drop1" @dragover="allowDrop">
                <hr>
            </div>

            <div id="box-droppable2" @drop="drop2" @dragover="allowDrop">
                <hr>
            </div>
            <p v-if="showTrue === 2" id="correct-answer">נכון מאוד!</p>
            <p v-if="showFalse === 2" id="incorrect-answer">לא נכון!</p>
            
        </div>

        <div id="second" v-show="!showFirst">
            <div id="question">דימוי עצמי נמוך מתבטא כחלק ממימד</div>
            <div id="container">
                <div id="draggable1">
                    <div class="" :draggable="noOneDrag" @dragstart="onDragging" id="11">
                        <p>רגשי</p>
                    </div>
                </div>
                <div id="draggable2">
                    <div class="" :draggable="noOneDrag" @dragstart="onDragging" id="12">
                        <p>חברתי</p>
                    </div>
                </div>
                <div id="draggable3">
                    <div class="" :draggable="noOneDrag" @dragstart="onDragging" id="13">
                        <p>התנהגותי</p>
                    </div>
                </div>
            </div>

            <div id="droppable" @drop="drop1" @dragover="allowDrop">
                <hr>
            </div>

            <p v-if="showTrueTwo" id="correct-answer">נכון מאוד!</p>
            <p v-if="showFalseTwo" id="incorrect-answer">לא נכון!</p>
        </div>
    </div>
  </template>
     
  <script>
  
  
  export default {
    name: "drag-question",
    components: {},
    props: ['typeQuestion'],
    data() {
      return {
        showTrue: false,
        showFalse: false,
        showFirst: false,
        noOneDrag: true,
        showTrueTwo: false,
        showFalseTwo: false
      };
    },
    methods: {
        onDragging(ev) {
            ev.dataTransfer.setData("text", ev.target.id);
        },
        allowDrop(ev) {
            ev.preventDefault();
        },
        drag(ev) {
            ev.dataTransfer.setData("text", ev.target.id);
        },
        drop1(ev) {
            ev.preventDefault();
            let data = ev.dataTransfer.getData("text");
            ev.target.appendChild(document.getElementById(data));
            this.imgShow = false;
            if(data === '1') {
                this.showTrue++;
            }
            else if(data === '11') {
                this.noOneDrag = false;
                this.showTrueTwo = true;
            }
            else if(data === '12' || data === '13') {
                this.noOneDrag = false;
                this.showFalseTwo = true;
            }
            else {
                this.showFalse++;
            }
            
        },
        drop2(ev) {
            ev.preventDefault();
            let data = ev.dataTransfer.getData("text");
            ev.target.appendChild(document.getElementById(data));
            this.imgShow = false;
            if(data === '2') {
                this.showTrue++;
            }
            else {
                this.showFalse++;
            }
            
        },
  
    },
    mounted() {
      
    }
  }
  
  
  </script>
    
<style scoped>
#dragQuestion {
    background-color: aqua;
    height: 34vh;
    width: 39vw;
    position: absolute;
    top: 29vh;
    left: 32vw;
}


#droppable {
    position: absolute;
    top: 15vh;
    left: 13vw;
    width: 10vw;
    height: 5vh;
}

#question {
    position: absolute;
    top: 2vh;
    left: 11vw;
    font-size: 2.5vh;
}

#draggable1,
#draggable2,
#draggable3 {
    position: absolute;
    top: 20vh;
    font-size: 2vh;
}

#draggable1 {
    left: 5vw;
}

#draggable2 {
    left: 17vw;
}

#draggable3 {
    left: 30vw;
}

#correct-answer {
    color: rgb(56, 156, 101);
}

#incorrect-answer {
    color: rgb(199, 52, 52);
}

#incorrect-answer, 
#correct-answer {
    position: absolute;
    top: 23vh;
    left: 16vw;
    font-size: 3vh;
}

#draggable-container{
    width: 10vw;
    position: absolute;
    left: 8vw;
    top: 3.5vh;
    /* background-color: rgb(197, 59, 59); */
}

#draggable-container2{
    width: 10vw;
    position: absolute;
    left: 20vw;
    top: 3.5vh;
    /* background-color: rgb(255, 255, 255); */
}

#box-droppable1 {
  width: 10vw;
  height: 4vh;
  position: absolute;
  left: 1.5vw;
  top: 26vh;
  /* background-color: rgb(197, 59, 59); */
}

#box-droppable2 {
  width: 10vw;
  height: 4vh;
  position: absolute;
  left: 25vw;
  top: 26vh;
  /* background-color: rgb(255, 255, 255); */
}

#firstQuestion {
    position: absolute;
    top: 25vh;
    left: 5vw;
    font-weight: bold;
}

#secondQuestion {
    position: absolute;
    top: 25vh;
    left: 28vw;
    font-weight: bold;
}

#names {
    position: absolute;
    left: 5vw;
}
</style>
  