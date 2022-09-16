<template>
  <div class="suggest">
    <button @click="handleClick" :class="{ disabled: this.suggest.disabled }">
      +{{ this.suggest.times }} suggest
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
.suggest {
  position: fixed;
  top: 10%;
  right: 10%;
  button {
    cursor: pointer;
    color: white;
    border: 0.5px solid currentColor;
    border-radius: 6px;
    padding: 12px 16px;
    background: transparent;
    font-size: 14px;
    outline: none;
    transition: all 0.3s linear;
    &:hover {
      color: var(--yellow);
    }
    &.disabled {
      cursor: default;
      pointer-events: none;
      color: var(--gray);
    }
  }
}
</style>
