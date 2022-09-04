<template>
  <div class="main" :style="gridStyles">
    <Cell
      v-for="cell in duplicateArr(pokemonList)"
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
      limit: (this.totalColumn * this.totalColumn) / 2,
    }
  },
  methods: {
    getPokemon() {
      return axios.get(
        `https://pokeapi.co/api/v2/pokemon?limit=${this.limit}&offset=0`
      )
    },
    duplicateArr(array) {
      const duplicate = [...array, ...array]
      return duplicate
    },
  },
  created() {
    this.getPokemon().then((res) => {
      res.data.results.forEach(async (pokemon) => {
        const poke = await axios.get(
          `https://pokeapi.co/api/v2/pokemon/${pokemon.name}`
        )
        this.pokemonList.push(poke)
      })
    })
  },
  computed: {
    cellStyles() {
      return {
        height: `${35 / this.totalColumn}rem`,
        width: `${35 / this.totalColumn}rem`,
      }
    },
    gridStyles() {
      return {
        'grid-template-rows': 'repeat(' + this.totalColumn + ', 1fr)',
        'grid-template-columns': 'repeat(' + this.totalColumn + ', 1fr)',
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
