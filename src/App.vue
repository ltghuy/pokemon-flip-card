<template>
  <welcome-screen
    v-if="gameStatus === 'default'"
    @onStart="handleStartGame($event)"
  />
  <main-screen
    v-if="gameStatus === 'playing'"
    :totalColumn="this.totalColumn"
  />
</template>

<script>
import WelcomeScreen from './components/WelcomeScreen.vue'
import MainScreen from './components/MainScreen.vue'

export default {
  name: 'App',
  components: {
    WelcomeScreen,
    MainScreen,
  },
  data() {
    return {
      gameStatus: 'default',
      totalColumn: 0,
    }
  },
  methods: {
    handleStartGame(config) {
      this.totalColumn = config.totalColumn
      this.gameStatus = 'playing'
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
