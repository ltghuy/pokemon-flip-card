<template>
  <div class="welcome">
    <div class="wrapper">
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
    <div class="question" v-if="showModal" @click.self="closeModalBox">
      <div class="box">
        <h3 class="title">Do you want to play games in full screen?</h3>
        <div class="choose">
          <button class="hightlight" @click="showFullScreen">Yes</button>
          <button @click="closeModalBox">No</button>
        </div>
      </div>
    </div>
    <div class="dim"></div>
  </div>
</template>

<script>
export default {
  emits: ['onStart'],
  data() {
    return {
      showModal: false,
    }
  },
  methods: {
    onStart(totalColumn) {
      this.$emit('onStart', { totalColumn })
    },
    showFullScreen() {
      const ele = document.documentElement
      if (ele.requestFullscreen) {
        ele.requestFullscreen()
      }
      this.showModal = false
    },
    showModalBox() {
      setTimeout(() => {
        this.showModal = true
      }, 800)
    },
    closeModalBox() {
      this.showModal = false
    },
  },
  mounted() {
    this.showModalBox()
  },
}
</script>

<style lang="scss" scoped>
@use '../assets/styles/breakpoints.scss' as *;
.welcome {
  background: url('../../public/images/pokemon-bg.jpg') center/cover;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  position: relative;
  .wrapper {
    text-align: center;
    z-index: 2;
  }
  h1 {
    color: var(--yellow);
    text-transform: uppercase;
    font-size: 4rem;
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
  .question {
    background-color: rgb(0 0 0 / 65%);
    position: absolute;
    inset: 0;
    z-index: 2;
    display: flex;
    align-items: center;
    justify-content: center;
    .box {
      animation: slideDown 1.2s cubic-bezier(0.175, 0.885, 0.32, 1.275);
      border-radius: 1rem;
      background-color: var(--white);
      box-shadow: 0 0 10px 5px #666;
      padding: 5rem 1rem 8rem;
      text-align: center;
    }
    .title {
      color: var(--dark);
      font-size: 1.5em;
      display: block;
    }
    .choose {
      padding-top: 6rem;
      display: flex;
      justify-content: center;
      column-gap: 1rem;
      button {
        border-radius: 0.5rem;
        border: 1px solid var(--dark);
        background-color: var(--dark);
        color: var(--light);
        cursor: pointer;
        font-size: 1rem;
        padding: 0.5rem 2.5rem;
        outline: none;
        transition: all 0.2s linear;
        &.hightlight {
          background-color: var(--yellow);
          border-color: var(--yellow);
        }
        &:hover {
          background-color: var(--white);
          border-color: var(--dark);
          color: var(--dark);
        }
      }
    }
  }
  .dim {
    background-color: rgb(0 0 0 / 65%);
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
  }

  @media screen and (max-width: $lg) {
    background: url('../../public/images/pokemon-bg-tablet.jpg') center/cover;
  }

  @media screen and (max-width: $md) {
    background: url('../../public/images/pokemon-bg-mobile.jpg') center/cover;
    .options {
      button {
        width: 8rem;
        height: 8rem;
      }
    }
    .question {
      display: none;
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
      width: 7rem;
      height: 7rem;
      font-size: 1rem;
    }
  }
  @keyframes slideDown {
    from {
      transform: translateY(-100%);
      opacity: 0;
    }
    to {
      transform: translateY(0);
      opacity: 1;
    }
  }
}
</style>
