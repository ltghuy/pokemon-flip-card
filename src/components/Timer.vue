<template>
  <div class="timer">
    <div
      class="progress"
      :style="{ width: (currentTimer / duration) * 100 + '%' }"
    ></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      duration: 300,
      currentTimer: 300,
    }
  },
  methods: {
    countDownTimer() {
      if (this.currentTimer > 0) {
        setTimeout(() => {
          this.currentTimer -= 1
          this.countDownTimer()
        }, 1000)
      } else {
        setTimeout(() => {
          alert('Time Over !!!')
          this.$emit('onTimeOver')
        }, 1000)
      }
    },
  },
  created() {
    this.countDownTimer()
  },
}
</script>

<style scoped lang="scss">
.timer {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  width: 100%;
  height: 5px;
  background-color: var(--light);
  .progress {
    position: absolute;
    top: 0;
    left: 0;
    height: 100%;
    width: 200px;
    background: linear-gradient(62deg, #fbab7e 0%, #f7ce68 100%);
    transition: width 0.2s linear;
  }
}
</style>
