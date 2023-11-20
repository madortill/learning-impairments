<template>
    <div id="endScreen">
      <div class="text" > כל הכבוד לכם !</div>
      <div class="text">סיימתם את הלומדה בהצלחה</div>
    </div>
  </template>
     
  <script>
  
  
  export default {
    name: "end-screen",
    components: {},
    data() {
      return {
      };
    },
    methods: {
  
    },
    mounted() {
      
    }
  }
  
  
  </script>
    
<style scoped>
#endScreen {
    background-image: url("../assets/images/classroom.svg");
    background-repeat: no-repeat;
    background-size: 170vw 170vh;
    background-position: 50% 80%;
    height: 100vh;
    width: 100vw;
    direction: rtl;
    display: flex;
    flex-direction: column;
    flex-wrap: nowrap;
    justify-content: center;
    align-items: center;
}


.text{
  text-align: center;
  font-size: 5vh;
  color: white;
}
</style>
  