<template>
  <div class="ignore">
    <img :src="`student${studentNum}.svg`" :class="`stud${studentNum}`" @click="openStudent"
    :style="countGrey !== 0.9 ? '': 'cursor: default'">
  </div>
</template>
     
<script>
// import '@/assets/student0.svg'
// import '@/assets/student1.svg'
// import '@/assets/student2.svg'
// import '@/assets/student3.svg'

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
  margin-top: -2vh;
  width: 25vw;
  filter: grayscale(v-bind(countGrey));
}
.stud1 {
  margin-top: -5vh;
  width: 21vw;
  filter: grayscale(v-bind(countGrey));
}
.stud2 {
  width: 20vw;
  filter: grayscale(v-bind(countGrey));
}
.stud3 {
  margin-top: -1vh;
  width: 23vw;
  filter: grayscale(v-bind(countGrey));
}

.ignore {
  display: contents;
}
</style>
  