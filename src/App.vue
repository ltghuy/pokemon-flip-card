<template>
  <welcome-screen
    v-if="gameStatus === 'default'"
    @onStart="handleStartGame($event)"
  />
  <main-screen
    v-if="gameStatus === 'playing'"
    :totalColumn="this.totalColumn"
    @onFinish="onGetResult"
    @onTimeOver="onRestart"
  />
  <result-screen
    v-if="gameStatus === 'result'"
    @onRestart="onRestart"
    :timer="this.timer"
  />
</template>

<script>
import WelcomeScreen from './components/WelcomeScreen.vue'
import MainScreen from './components/MainScreen.vue'
import ResultScreen from './components/ResultScreen.vue'

export default {
  name: 'App',
  components: {
    WelcomeScreen,
    MainScreen,
    ResultScreen,
  },
  data() {
    return {
      gameStatus: 'default',
      totalColumn: 0,
      startedAt: null,
      timer: 0,
    }
  },
  methods: {
    handleStartGame(config) {
      this.totalColumn = config.totalColumn
      this.startedAt = new Date().getTime()
      this.gameStatus = 'playing'
    },
    onGetResult() {
      this.gameStatus = 'result'
      this.timer = new Date().getTime() - this.startedAt
    },
    onRestart() {
      this.gameStatus = 'default'
    },
  },
}
</script>

<style lang="scss">
#app {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
