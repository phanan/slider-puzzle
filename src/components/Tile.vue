<template>
  <div class="tile" :style="tile.styles" @click="move" />
</template>

<script>
export default {
  props: ['tile'],

  methods: {
    move () {
      this.$emit('moving', this.tile)
    }
  }
}
</script>

<style lang="scss">
.tile {
  border: 1px solid #111;
  transition: border .3s;

  &:hover {
    border-color: blue;
    cursor: pointer;
  }
}
</style>
