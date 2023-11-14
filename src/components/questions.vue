<template>
    <div id="questions">
        <dragQuestion @finished="next" :typeQuestion="10" v-if="currQuestion === 10"></dragQuestion>
        <dragQuestion @finished="next" :typeQuestion="11" v-if="currQuestion === 11"></dragQuestion>
        <openQuestion :question="question" @finished="next" v-if="currQuestion >= 2  && currQuestion <= 5"></openQuestion>
        <multipleChoiceQuestion :question="question" @finished="next" v-if="currQuestion === 7 || currQuestion === 6"></multipleChoiceQuestion>
        <trueOrFalse :question="question" @finished="next" v-if="currQuestion === 1"></trueOrFalse>
    </div>
  </template>
     
  <script>
  import json from '@/data.json';
  import dragQuestion from '@/components/dragQuestion.vue'  
  import openQuestion from '@/components/openQuestion.vue'  
  import multipleChoiceQuestion from '@/components/multipleChoiceQuestion.vue'  
  import trueOrFalse from '@/components/trueOrFalse.vue' 
  
  
  export default {
    name: "questions",
    components: {dragQuestion, openQuestion, multipleChoiceQuestion, trueOrFalse},
    props: ["type"],
    data() {
      return {
        currQuestion: this.type
      };
    },
    methods: {
        next() {
          this.$emit('finishQuestion');
        }
    },
    computed: {
      question() {
        return (json["questions"][0][this.currQuestion]);
      }
    },
    mounted() {
    }
  }
  
  
  </script>
    
<style scoped>
#question {
  position: absolute;
  z-index: 3;
}
</style>
  