<template>
  <div class="tile" :style="tile.styles" @click="move" :class="{ empty: tile.isEmpty }" />
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

  &.empty {
    box-shadow: rgba(0, 0, 0, 0.5) 0px 5px 10px inset;
    background: transparent !important;

    &:hover {
      border-color: #111;
      cursor: default;
    }
  }

  &:hover {
    border-color: white;
    cursor: pointer;
  }
}
</style>
