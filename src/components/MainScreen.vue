<template>
  <div class="main" :style="gridStyles">
    <Cell
      v-for="cell in fullList"
      :key="cell.data.id"
      :style="cellStyles"
      :id="cell.data.id"
    />
    <div v-if="loading" class="loading">
      <div class="circle-container">
        <img class="type" src="/images/dark.png" alt="dark" />
        <img class="type" src="/images/electric.png" alt="electric" />
        <img class="type" src="/images/fairy.png" alt="fairy" />
        <img class="type" src="/images/fire.png" alt="fire" />
        <img class="type" src="/images/grass.png" alt="grass" />
        <img class="type" src="/images/ice.png" alt="ice" />
        <img class="type" src="/images/normal.png" alt="normal" />
        <img class="type" src="/images/psychic.png" alt="psychic" />
        <img class="type" src="/images/water.png" alt="water" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Cell from './Cell.vue'

export default {
  components: {
    Cell,
  },
  props: {
    totalColumn: Number,
  },
  data() {
    return {
      pokemonList: [],
      fullList: [],
      loading: true,
      limit: (this.totalColumn * this.totalColumn) / 2,
      offset: Math.floor(Math.random() * 100),
    }
  },
  methods: {
    getPokemon() {
      return axios.get(
        `https://pokeapi.co/api/v2/pokemon?limit=${this.limit}&offset=${this.offset}`
      )
    },
    shuffle() {
      this.fullList.sort(() => Math.random() - 0.5)
    },
  },
  created() {
    this.getPokemon().then((res) => {
      res.data.results.forEach(async (pokemon) => {
        const poke = await axios.get(
          `https://pokeapi.co/api/v2/pokemon/${pokemon.name}`
        )
        this.pokemonList.push(poke)
        setTimeout(() => {
          this.fullList = [...this.pokemonList, poke]
          this.shuffle()
          this.loading = false
        }, 10000)
      })
    })
  },
  computed: {
    cellStyles() {
      return {
        height: `${35 / this.totalColumn}rem`,
        width: `${35 / this.totalColumn}rem`,
        'border-radius': `${2 / this.totalColumn}rem`,
      }
    },
    gridStyles() {
      return {
        'grid-template-rows': 'repeat(' + this.totalColumn + ', 1fr)',
        'grid-template-columns': 'repeat(' + this.totalColumn + ', 1fr)',
        gap: `${5 / this.totalColumn}rem`,
      }
    },
  },
}
</script>

<style scoped lang="scss">
@mixin on-circle($item-count, $circle-size, $item-size) {
  position: relative;
  width: $circle-size;
  height: $circle-size;
  border-radius: 50%;

  > * {
    display: block;
    position: absolute;
    top: 50%;
    left: 50%;
    width: $item-size;
    height: $item-size;
    margin: -($item-size / 2);

    $angle: (360 / $item-count);
    $rot: 0;

    @for $i from 1 through $item-count {
      &:nth-of-type(#{$i}) {
        transform: rotate($rot * 1deg)
          translate($circle-size / 2)
          rotate($rot * -1deg);
      }

      $rot: $rot + $angle;
    }
  }
}

@keyframes rotate360 {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.main {
  display: grid;

  .loading {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    display: flex;
    justify-content: center;
    align-items: center;

    .circle-container {
      @include on-circle($item-count: 9, $circle-size: 20em, $item-size: 4em);
      animation: rotate360 8s linear infinite;
      img {
        display: block;
        max-width: 100%;
        filter: drop-shadow(0px 0px 10px rgb(225, 225, 225));
        user-select: none;
      }
    }
  }
}
</style>
