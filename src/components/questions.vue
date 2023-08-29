<template>
    <div id="questions">
        <dragQuestion @finished="next" v-if="currQuestion"></dragQuestion>
        <openQuestion :question="question" @finished="next" v-if="currQuestion"></openQuestion>
        <multipleChoiceQuestion :question="question" @finished="next" v-if="currQuestion"></multipleChoiceQuestion>
        <trueOrFalse :question="question" @finished="next" v-if="currQuestion"></trueOrFalse>
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
        currQuestion: type
      };
    },
    methods: {
        next() {
            this.$emit('next-page');
        }
    },
    computed: {
      question() {
        return (json["questions"][0][this.currQuestion]);
      }
    },
    mounted() {
      // console.log(this.question);
    }
  }
  
  
  </script>
    
<style scoped>

</style>
  