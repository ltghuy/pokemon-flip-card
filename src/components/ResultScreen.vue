<template>
  <div class="result">
    <h1 class="text">✨Congratulations✨</h1>
    <h3 class="timer">{{ Math.round(timer / 920) }} seconds</h3>
    <button class="button" @click="handleRestart">Start again</button>
  </div>
</template>

<script>
export default {
  props: {
    timer: {
      type: Number,
      default: 0,
    },
  },
  methods: {
    handleRestart() {
      this.$emit('onRestart')
    },
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
