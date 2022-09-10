<template>
  <div class="main" :style="gridStyles">
    <Cell
      v-for="cell in fullList"
      :key="cell.data.id"
      :style="cellStyles"
      :id="cell.data.id"
    />
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
        }, 5000)
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
.main {
  display: grid;
}
</style>
