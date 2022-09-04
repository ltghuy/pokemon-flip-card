<template>
  <div class="main">
    <div v-for="column in totalColumn" :key="column">
      <div v-for="column in totalColumn" :key="column" :style="cellStyles">
        <Cell />
      </div>
    </div>
  </div>
</template>

<script>
import Cell from './Cell.vue'

export default {
  components: {
    Cell,
  },
  props: {
    totalColumn: Number,
  },
  computed: {
    cellStyles() {
      return {
        height: `${35 / this.totalColumn}rem`,
        width: `${35 / this.totalColumn}rem`,
        'margin-bottom': `1rem`,
      }
    },
  },
}
</script>

<style scoped lang="scss">
.main {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 1rem;
}
</style>
