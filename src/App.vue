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
  <div class="features">
    <gallery :collection="this.collection" />
    <div class="music">
      <button @click="triggerAudio" :class="{ playing: sound }">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="ionicon"
          viewBox="0 0 512 512"
        >
          <path
            d="M192 218v-6c0-14.84 10-27 24.24-30.59l174.59-46.68A20 20 0 01416 154v22"
            fill="none"
            stroke="currentColor"
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="32"
          />
          <path
            d="M416 295.94v80c0 13.91-8.93 25.59-22 30l-22 8c-25.9 8.72-52-10.42-52-38h0a33.37 33.37 0 0123-32l51-18.15c13.07-4.4 22-15.94 22-29.85V58a10 10 0 00-12.6-9.61L204 102a16.48 16.48 0 00-12 16v226c0 13.91-8.93 25.6-22 30l-52 18c-13.88 4.68-22 17.22-22 32h0c0 27.58 26.52 46.55 52 38l22-8c13.07-4.4 22-16.08 22-30v-80"
            fill="none"
            stroke="currentColor"
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="32"
          />
        </svg>
      </button>
      <audio id="audio" src="audios/theme-song.mp3" loop></audio>
    </div>
  </div>
</template>

<script>
import WelcomeScreen from './components/WelcomeScreen.vue'
import MainScreen from './components/MainScreen.vue'
import ResultScreen from './components/ResultScreen.vue'
import Gallery from './components/Gallery.vue'

export default {
  name: 'App',
  components: {
    WelcomeScreen,
    MainScreen,
    ResultScreen,
    Gallery,
  },
  data() {
    return {
      gameStatus: 'default',
      totalColumn: 0,
      startedAt: null,
      timer: 0,
      sound: false,
      collection: 1,
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
      this.startedAt = null
    },
    triggerAudio() {
      const audio = document.getElementById('audio')
      this.sound = !this.sound
      if (this.sound) {
        audio.play()
      } else {
        audio.pause()
        audio.currentTime = 0
      }
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
  position: relative;
  .features {
    position: absolute;
    top: 20px;
    right: 20px;
    display: flex;
    align-items: center;
  }
  .music {
    margin-left: 1rem;
    button {
      cursor: pointer;
      border: 0;
      border-radius: 50%;
      background: #c0c0c03d;
      width: 40px;
      height: 40px;
      display: flex;
      justify-content: center;
      align-items: center;
      outline: none;
      &.playing {
        svg {
          color: var(--yellow);
        }
      }
    }
    svg {
      color: var(--white);
      width: 20px;
    }
  }
}
</style>
