<template>
  <div class="welcome">
    <h1>Poke Memories</h1>
    <h3>Select mode to start game</h3>
    <div class="options">
      <button @click="onStart(4)">
        <span>4 x 4</span>
        Easy
      </button>
      <button @click="onStart(6)">
        <span>6 x 6</span>
        Normal
      </button>
      <button @click="onStart(8)">
        <span>8 x 8</span>
        Hard
      </button>
      <button @click="onStart(10)">
        <span>10 x 10</span>
        Super Hard
      </button>
    </div>
  </div>
</template>

<script>
export default {
  emits: ['onStart'],
  methods: {
    onStart(totalColumn) {
      this.$emit('onStart', { totalColumn })
    },
  },
}
</script>

<style lang="scss" scoped>
@use '../assets/styles/breakpoints.scss' as *;
.welcome {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  h1 {
    color: var(--yellow);
    text-transform: uppercase;
    font-size: 4rem;
    text-align: center;
    margin-bottom: 1rem;
  }
  h3 {
    font-size: 2rem;
  }
  .options {
    margin-top: 2rem;
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    button {
      background-color: transparent;
      border: 1px solid currentColor;
      border-radius: 1.5rem;
      cursor: pointer;
      color: var(--light);
      width: 10rem;
      height: 10rem;
      margin: 1rem;
      font-size: 1.4rem;
      font-family: 'Odibee Sans', cursive;
      transition: all 0.2s;
      span {
        display: block;
        font-size: 2rem;
        margin-bottom: 0.5rem;
      }

      &:hover {
        color: var(--dark);
        background-color: var(--light);
      }
    }
  }
  @media screen and (max-width: $sm) {
    h1 {
      font-size: 3rem;
    }
    h3 {
      font-size: 1.5rem;
    }
    .options button {
      width: 8rem;
      height: 8rem;
    }
  }
}
</style>
