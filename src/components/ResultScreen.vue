<template>
  <div class="result">
    <h1 class="text">🎉You won!🎉</h1>
    <h3 class="timer">
      {{ `${this.minutes} m ${this.seconds} s` }}
    </h3>
    <button class="button" @click="handleRestart">Continue</button>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  props: {
    timer: {
      type: Number,
      default: 0,
    },
  },
  data() {
    return {
      minutes: Math.floor(this.timer / 920 / 60),
      seconds: Math.floor((this.timer / 920) % 60),
      timeout: null,
    }
  },
  methods: {
    handleRestart() {
      this.$emit('onRestart')
    },
    showAlertUnLock() {
      const collection = Number(localStorage.getItem('pokemonCollection'))
      localStorage.setItem('pokemonCollection', collection + 1)
      this.timeout = setTimeout(() => {
        axios
          .get(`https://pokeapi.co/api/v2/pokemon/${collection + 1}`)
          .then((res) => {
            const pokemon = String(res.data.name)
            alert(`Unlock successfully: ${pokemon.toUpperCase()}`)
          })
      }, 1500)
    },
  },
  mounted() {
    this.showAlertUnLock()
  },
  beforeUnmount() {
    clearTimeout(this.timeout)
  },
}
</script>

<style lang="scss" scoped>
.result {
  color: var(--white);
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  .text {
    font-size: 4rem;
  }
  .timer {
    font-size: 2rem;
    margin: 2rem;
  }
  .button {
    background: transparent;
    border: 1px solid currentColor;
    border-radius: 8px;
    cursor: pointer;
    color: white;
    font-size: 1.2rem;
    padding: 1rem 2rem;
    transition: all 0.2s;
    &:hover {
      color: var(--yellow);
    }
  }
}
</style>
