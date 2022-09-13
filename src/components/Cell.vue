<template>
  <div class="cell" :class="{ disabled: isDisabled }" @click="handleFlipCard">
    <div class="content" :class="{ flip: isFliped }">
      <div class="back">
        <img src="/images/pokeball.png" alt="pokeball" />
      </div>
      <div class="front">
        <img
          v-if="this.card.value < 10"
          :src="imgPokemon('00', this.card.value)"
          :alt="pokemon"
        />
        <img
          v-else-if="this.card.value < 100"
          :src="imgPokemon('0', this.card.value)"
          :alt="pokemon"
        />
        <img v-else :src="imgPokemon('', this.card.value)" :alt="pokemon" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isFliped: false,
      isDisabled: false,
      imgPokemon: (n, id) =>
        'https://assets.pokemon.com/assets/cms2/img/pokedex/full/' +
        n +
        id +
        '.png',
    }
  },
  props: {
    card: Object,
    rules: Array,
  },
  methods: {
    handleFlipCard() {
      if (this.rules.length >= 2) return
      if (this.isDisabled) return
      this.isFliped = !this.isFliped
      if (this.isFliped) {
        this.$emit('onFlip', this.card)
      }
    },
    onFlipBackCard() {
      this.isFliped = false
    },
    onLockFlip() {
      this.isDisabled = true
    },
  },
}
</script>

<style scoped lang="scss">
.cell {
  border: 1px solid var(--gray);
  cursor: pointer;
  width: 100%;
  height: 100%;
  position: relative;
  perspective: 30rem;

  &.disabled {
    cursor: default;
    border: 1px solid var(--blue);
  }

  &:hover {
    .back {
      background-color: #a7d2f766;
    }
  }

  .content {
    border-radius: inherit;
    position: absolute;
    width: 100%;
    height: 100%;
    box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
    transition: transform 1s;
    transform-style: preserve-3d;
    transition: transform 0.5s;
    transform: rotateY(-180deg);
    &.flip {
      transform: rotateY(0deg);
    }
  }

  .front,
  .back {
    border-radius: inherit;
    position: absolute;
    height: 100%;
    width: 100%;
    background: transparent;
    backface-visibility: hidden;
    display: flex;
    justify-content: center;
    align-items: center;
    img {
      width: 80%;
      height: 80%;
      object-fit: cover;
    }
  }

  .back {
    transform: rotateY(-180deg);
    transition: all 0.3s;
  }
}
</style>
