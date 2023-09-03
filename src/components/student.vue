<template>
  <div class="ignore">
    <img src="/student.png" class="stud" @click="openStudent">
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
    finish: Boolean
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
  