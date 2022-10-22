<template>
  <button @click="openCollection" class="galleryBtn">👑</button>
  <div
    v-if="this.showCollection"
    class="collection"
    @click.self="closeCollection"
  >
    <div class="cards">
      <div class="card grass">
        <div class="wrapper">
          <img
            src="https://i0.wp.com/yumetwinsblog.wpcomstaging.com/wp-content/uploads/2021/12/bb4bccb5-7a06-4b30-be9d-5ea3f461873e_3.png?w=620&ssl=1"
            alt="pokemon"
          />
          <div class="description">
            {{ collection }}
          </div>
        </div>
      </div>
      <div class="card electric">
        <div class="wrapper">
          <img
            src="https://freepngimg.com/thumb/pokemon/20346-7-pokemon-hd.png"
            alt="pokemon"
          />
          <div class="description">
            {{ collection }}
          </div>
        </div>
      </div>
      <div class="card fire">
        <div class="wrapper">
          <img
            src="https://i.pinimg.com/originals/f2/95/76/f295769d9bd3c34ffc552e837f5304ae.png"
            alt="pokemon"
          />
          <div class="description">
            {{ collection }}
          </div>
        </div>
      </div>
      <div class="card water">
        <div class="wrapper">
          <img
            src="https://assets.webiconspng.com/uploads/2017/09/Pokemon-PNG-Image-48368.png"
            alt="pokemon"
          />
          <div class="description">
            {{ collection }}
          </div>
        </div>
      </div>
      <div class="card dark">
        <div class="wrapper">
          <img
            src="https://static.pokemonpets.com/images/monsters-images-800-800/94-Gengar.png"
            alt="pokemon"
          />
          <div class="description">
            {{ collection }}
          </div>
        </div>
      </div>
      <div class="card fairy">
        <div class="wrapper">
          <img
            src="https://oyster.ignimgs.com/mediawiki/apis.ign.com/pokemon-x-y-version/2/2c/Vivillon_official_art_transparent_background.png?width=1280"
            alt="pokemon"
          />
          <div class="description">
            {{ collection }}
          </div>
        </div>
      </div>
      <div class="card normal">
        <div class="wrapper">
          <img
            src="https://qph.cf2.quoracdn.net/main-qimg-f035080bc60124c8a64ef1a84b58aa95"
            alt="pokemon"
          />
          <div class="description">
            {{ collection }}
          </div>
        </div>
      </div>
      <div class="card ice">
        <div class="wrapper">
          <img
            src="https://cdn.shortpixel.ai/spai/w_381+q_lossy+ret_img+to_webp/https://pokeweakness.com/images/1892690-144articuno.png"
            alt="pokemon"
          />
          <div class="description">
            {{ collection }}
          </div>
        </div>
      </div>
      <div class="card psychic">
        <div class="wrapper">
          <img
            src="https://www.gamerguides.com/assets/media/11/151/151-3.png"
            alt="pokemon"
          />
          <div class="description">
            {{ collection }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    collection: Number,
  },
  data() {
    return {
      showCollection: false,
    }
  },
  methods: {
    openCollection() {
      this.showCollection = true
    },
    closeCollection() {
      this.showCollection = false
    },
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
    animation: zoomIn 0.5s cubic-bezier(0, 0.0015, 0.55, 0.35);
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
      height: 40%;
      flex-shrink: 0;
      filter: drop-shadow(6px 2px 10px white);
      object-fit: cover;
      padding: 0.5rem;
    }
    .description {
      flex: 1;
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
    width: 80%;
    height: 80%;
    opacity: 1;
  }
}
</style>
