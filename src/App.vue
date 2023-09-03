<template>
    <div class="wrapper">
      <open-screen v-if="screen === 1" @done="switchScreen"></open-screen>
      <main-screen v-if="screen === 2" @done="switchScreen"></main-screen>
      <endScreen v-if="screen === 3" @done="switchScreen"></endScreen>
    </div>
</template>

<script>
import openScreen from './components/openScreen.vue'
import mainScreen from './components/mainScreen.vue'
import endScreen from './components/endScreen.vue'

export default {
  name: "app",
  components: { openScreen, mainScreen, endScreen},
  data() {
    return {
      screen: 2,
    };
  },
  methods: {
    switchScreen() {
      this.screen === 3 ? this.screen = 1 : this.screen++;
    }
  }
}
</script>

<style scoped>

</style>
