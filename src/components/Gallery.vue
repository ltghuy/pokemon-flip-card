<template>
  <button @click="openCollection" class="galleryBtn">👑</button>
  <div
    v-if="this.showCollection"
    class="collection"
    @click.self="closeCollection"
  >
    <div class="cards">
      <div
        class="card"
        :class="pokemon.data.types[0].type.name"
        v-for="pokemon in pokemonCollection"
        :key="pokemon.data.id"
      >
        <div class="wrapper">
          <img
            v-if="pokemon.data.id < 10"
            :src="imgPokemon('00', pokemon.data.id)"
            :alt="pokemon.data.name"
          />
          <img
            v-else-if="pokemon.data.id < 100"
            :src="imgPokemon('0', pokemon.data.id)"
            :alt="pokemon.data.name"
          />
          <img
            v-else
            :src="imgPokemon('', pokemon.data.id)"
            :alt="pokemon.data.name"
          />
          <div class="description">
            <h3 class="name">{{ pokemon.data.name }}</h3>
            <p class="type">
              Type: <span>{{ pokemon.data.types[0].type.name }}</span>
            </p>
            <strong class="numID">{{ `#${pokemon.data.id}` }}</strong>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      collection: localStorage.getItem('pokemonCollection'),
      showCollection: false,
      pokemonCollection: [],
      imgPokemon: (n, id) =>
        'https://assets.pokemon.com/assets/cms2/img/pokedex/full/' +
        n +
        id +
        '.png',
    }
  },
  methods: {
    async getCollection() {
      return axios.get(
        `https://pokeapi.co/api/v2/pokemon?limit=${this.collection}`
      )
    },
    openCollection() {
      this.showCollection = true
    },
    closeCollection() {
      this.showCollection = false
    },
  },
  created() {
    this.getCollection().then((res) => {
      res.data.results.forEach(async (pokemon) => {
        const poke = await axios.get(
          `https://pokeapi.co/api/v2/pokemon/${pokemon.name}`
        )
        setTimeout(() => {
          this.pokemonCollection.push(poke)
          // Fix poke list not increasing by id
          this.pokemonCollection.sort(function (a, b) {
            if (a.data.id > b.data.id) return 1
            if (a.data.id < b.data.id) return -1
            return 0
          })
        }, 3000)
      })
    })
  },
}
</script>

<style lang="scss" scoped>
@use '../assets/styles/breakpoints.scss' as *;
.galleryBtn {
  border: 0;
  border-radius: 50%;
  background: #c0c0c03d;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 40px;
  height: 40px;
  font-size: 20px;
  user-select: none;
}
.collection {
  position: fixed;
  background-color: #00000045;
  display: flex;
  justify-content: center;
  align-items: center;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: 2;
  .cards {
    animation: zoomIn 0.5s cubic-bezier(0.215, 0.61, 0.355, 1);
    background-color: var(--white);
    border-radius: 1.2rem;
    box-shadow: 0px 0px 15px 10px #fcfcfc4f;
    position: relative;
    width: 75%;
    height: 65%;
    padding: 1rem;
    overflow-x: auto;
    overflow-y: hidden;
    white-space: nowrap;
    &::-webkit-scrollbar {
      display: none;
    }
  }
  .card {
    display: inline-block;
    width: 30%;
    height: 100%;
    border-radius: 0.5rem;
    margin: 0 0.5rem;
    @media screen and (max-width: $lg) {
      width: 45%;
    }
    @media screen and (max-width: $md) {
      width: 55%;
    }
    @media screen and (max-width: $sm) {
      width: 100%;
    }
    &:first-of-type {
      margin-left: 0;
    }
    &:last-of-type {
      margin-right: 0;
    }
  }
  .wrapper {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    img {
      border-top-left-radius: 0.5rem;
      border-top-right-radius: 0.5rem;
      height: 45%;
      flex-shrink: 0;
      filter: drop-shadow(6px 2px 10px white);
      object-fit: cover;
      padding: 0.5rem;
    }
    .description {
      flex: 1;
      width: 100%;
      margin-top: 1rem;
      text-align: center;
      text-transform: capitalize;
      background-color: #ffffff80;
      border-top-left-radius: 10rem;
      border-top-right-radius: 10rem;
      .name {
        color: var(--dark);
        font-size: 2.5rem;
        padding: 1.5rem 0rem 1rem;
      }
      .type {
        color: var(--dark);
        font-size: 1.2rem;
        span {
          margin-left: 0.5rem;
          padding: 0.2rem 1.2rem;
          background-color: var(--dark);
          border-radius: 10rem;
          color: var(--white);
        }
      }
      .numID {
        color: var(--dark);
        display: block;
        font-size: 1.2rem;
        margin-top: 2rem;
      }
    }
  }
}
@keyframes zoomIn {
  from {
    width: 0;
    height: 0;
    opacity: 0;
  }
  to {
    width: 75%;
    height: 65%;
    opacity: 1;
  }
}
</style>
