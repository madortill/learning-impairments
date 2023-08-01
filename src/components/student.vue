<template>
    <img id="student" :class="!isOpened ? blueC : greyC" @click="openStudent">
    <!-- <img :src="src" class="student" :id="!isOpened ? blue : grey" @click="openStudent"> -->
  </template>
     
  <script>
  
  
  export default {
    name: "student",
    components: {},
    props: ['isOpened'],
    data() {
      return {
        // src: require("@/assets/images/.png"),
      };
    },
    methods: {
        openStudent() {
            this.isOpened = true;
            // this.src = require("@/assets/images/.png");
        }
    },
    mounted() {
      
    }
  }
  
  
  </script>
    
<style scoped>
#student {
    height: 20vh;
    width: 8vw;
}

.blueC {
    background-color: rgb(122, 143, 238);
}
.greyC {
    background-color: rgb(105, 105, 105);
}
</style>
  