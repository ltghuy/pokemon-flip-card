<template>
  <div class="cell" @click="handleFlipCard">
    <div class="content" :class="{ flip: isFliped }">
      <div class="back">
        <img src="/images/pokeball.png" alt="pokeball" />
      </div>
      <div class="front">
        <img
          v-if="this.id < 10"
          :src="imgPokemon('00', this.id)"
          :alt="pokemon"
        />
        <img
          v-else-if="this.id < 100"
          :src="imgPokemon('0', this.id)"
          :alt="pokemon"
        />
        <img v-else :src="imgPokemon('', this.id)" :alt="pokemon" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isFliped: Boolean,
      imgPokemon: (n, id) =>
        'https://assets.pokemon.com/assets/cms2/img/pokedex/full/' +
        n +
        id +
        '.png',
    }
  },
  props: {
    id: Number,
  },
  methods: {
    handleFlipCard() {
      this.isFliped = !this.isFliped
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

  &:hover .back {
    background-color: #a7d2f766;
  }

  .content {
    border-radius: inherit;
    position: absolute;
    width: 100%;
    height: 100%;
    box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
    transition: transform 1s;
    transform-style: preserve-3d;
    &.flip {
      transform: rotateY(-180deg);
      transition: transform 0.5s;
    }
  }

  .front,
  .back {
    border-radius: inherit;
    position: absolute;
    height: 100%;
    width: 100%;
    background: var(--dark);
    backface-visibility: hidden;
    display: flex;
    justify-content: center;
    align-items: center;
    img {
      width: 80%;
      height: 80%;
      object-fit: cover;
      user-select: none;
    }
  }

  .back {
    transform: rotateY(-180deg);
    transition: all 0.3s;
  }
}
</style>
