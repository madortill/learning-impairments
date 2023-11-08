<template>
  <div class="ignore">
    <img :src="`/learning-impairments/student${studentNum}.svg`" :class="`stud${studentNum}`" @click="openStudent"
    :style="countGrey !== 0.9 ? '': 'cursor: default'">
  </div>
</template>
     
<script>
export default {
  name: "student",
  components: {},
  props: {
    countGrey: {
      type: Number,
      validator(value) {
        return (value === 0 || value === 0.9);
      }
    },
    finish: Boolean,
    studentNum: Number
  },
  methods: {
    openStudent() {
      // do not emit event if the student is grey
      if (this.finish && this.countGrey !== 0.9) {
        this.$emit("changeGrey");
      }
    },
  },
  mounted() {

  },
}


</script>
    
<style scoped>
.stud0 {
  /* margin-bottom: 3vh; */
  /* height: 26vh; */
  margin-top: -2vh;
  width: 25vw;
  filter: grayscale(v-bind(countGrey));
}
.stud1 {
  /* margin-bottom: 3vh; */
  /* height: 26vh; */
  margin-top: -5vh;
  width: 21vw;
  filter: grayscale(v-bind(countGrey));
}
.stud2 {
  /* margin-bottom: 3vh; */
  /* height: 26vh; */
  width: 20vw;
  filter: grayscale(v-bind(countGrey));
}
.stud3 {
  /* margin-bottom: 3vh; */
  /* height: 26vh; */
  margin-top: -1vh;
  width: 23vw;
  filter: grayscale(v-bind(countGrey));
}

.ignore {
  display: contents;
}
</style>
  