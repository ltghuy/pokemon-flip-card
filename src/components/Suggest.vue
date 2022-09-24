<template>
  <div class="suggest">
    <button @click="handleClick" :class="{ disabled: this.suggest.disabled }">
      <span>+{{ this.suggest.times }}</span>
      <svg
        xmlns="http://www.w3.org/2000/svg"
        shape-rendering="geometricPrecision"
        text-rendering="geometricPrecision"
        image-rendering="optimizeQuality"
        fill-rule="evenodd"
        clip-rule="evenodd"
        viewBox="0 0 512 417.79"
      >
        <path
          fill-rule="nonzero"
          d="M333.55 16.79 511 392.75c2.46 5.22.22 11.45-4.99 13.91-1.45.68-2.97 1.01-4.46 1l-177.77.03c-5.78 0-10.47-4.7-10.47-10.48V20.58c0-5.78 4.69-10.47 10.47-10.47 4.44 0 8.25 2.77 9.77 6.68zM240.3 402.16c0 18.18 26.25 21.89 30.98 3.74.28-1.29.45-2.4.45-3.74v-9.45c0-18.18-26.25-21.89-30.98-3.74-.28 1.29-.45 2.4-.45 3.74v9.45zm0-72.3c0 18.18 26.25 21.89 30.98 3.74.28-1.29.45-2.4.45-3.74v-31.42c0-18.18-26.25-21.89-30.98-3.74-.28 1.29-.45 2.4-.45 3.74v31.42zm0-94.27c0 18.18 26.25 21.89 30.98 3.74.28-1.29.45-2.4.45-3.74v-31.42c0-18.18-26.25-21.89-30.98-3.73-.28 1.28-.45 2.39-.45 3.73v31.42zm0-94.26c0 18.17 26.25 21.88 30.98 3.73.28-1.28.45-2.39.45-3.73V109.9c0-18.17-26.25-21.89-30.98-3.73-.28 1.28-.45 2.39-.45 3.73v31.43zm0-94.27c0 18.17 26.25 21.89 30.98 3.73.28-1.28.45-2.39.45-3.73V15.63c0-18.17-26.25-21.88-30.98-3.73-.28 1.29-.45 2.39-.45 3.73v31.43zM1.33 392.11 178.79 16.12c2.46-5.21 8.7-7.45 13.91-4.99 3.78 1.78 5.99 5.54 5.99 9.45l.04 376.63c0 5.78-4.7 10.48-10.48 10.48H10.48c-5.79 0-10.48-4.7-10.48-10.48 0-1.85.48-3.59 1.33-5.1zm483.72-5.37L334.26 67.26v319.48h150.79z"
        />
      </svg>
    </button>
  </div>
</template>

<script>
export default {
  props: {
    suggest: Object,
  },
  methods: {
    handleClick() {
      this.$emit('onSuggest')
    },
  },
}
</script>

<style scoped lang="scss">
@use '../assets/styles/breakpoints.scss' as *;
.suggest {
  position: absolute;
  top: 0;
  right: 0;
  transform: translateX(200%);
  button {
    cursor: pointer;
    color: var(--white);
    border: 0.5px solid currentColor;
    border-radius: 6px;
    padding: 10px 20px;
    background: transparent;
    font-size: 12px;
    outline: none;
    display: flex;
    align-items: center;
    transition: all 0.3s linear;
    svg {
      width: 16px;
      fill: currentColor;
      margin-left: 4px;
    }
    &:hover {
      color: var(--yellow);
    }
    &.disabled {
      cursor: default;
      color: var(--gray);
      pointer-events: none;
      user-select: none;
    }
  }
  @media screen and (max-width: $sm) {
    position: fixed;
    left: 50%;
    bottom: 50px;
    right: unset;
    top: unset;
    transform: translateX(-50%);
  }
}
</style>
