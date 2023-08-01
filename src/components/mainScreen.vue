<template>
    <div id="mainScreen">
      <div id="teacher"></div>
      <div id="box">
        <student v-for="(student, index) in mouses" :isOpened="student" :key="index" id=""></student>
      </div>
      
    </div>
  </template>
     
  <script>
  import student from '@/components/student.vue'
  
  export default {
    name: "main-screen",
    components: {student},
    data() {
      return {
        mouses: [false, false, false, false]
      };
    },
    methods: {
  
    },
    mounted() {
      
    }
  }
  
  
  </script>
    
<style scoped>
#mainScreen {
    background-image: url("../assets/images/classroom.jpg");
    background-repeat: no-repeat;
    background-size: 100vw 100vh;
    height: 100vh;
    width: 100vw;
}

#teacher {
    background-color: black;
    height: 40vh;
    width: 8vw;
    position: absolute;
    right: 72vw;
    top: 40vh;
}

#box {
    display: flex;
    justify-content: space-around;
    height: 100%;
    width: 100%;
    flex-wrap: wrap;
    align-content: flex-end;
    align-items: flex-start;
}
</style>
  