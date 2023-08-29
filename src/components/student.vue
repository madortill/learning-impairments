<template>
    <div class="ignore">
        <img :src="srcImg" class="stud" @click="openStudent">
    </div>
</template>
     
<script>

  
  export default {
    name: "student",
    components: {},
    props: ['countGrey', 'finish'],
    data() {
      return {
        srcImg: '/student.png'
      };
    },
    methods: {
        openStudent() {
          if(this.finish) {
            this.srcImg = '/student.png';
            this.$emit("changeGrey");
          }
      },
    },
    mounted() {
      
    },
  }
  
  
</script>
    
<style scoped>
.stud {
    margin-bottom: 3vh;
    height: 26vh;
    width: 9vw;
    margin-right: 13vw;
    filter: grayscale(v-bind(countGrey));
}

.ignore {
    display: contents;
}
</style>
  