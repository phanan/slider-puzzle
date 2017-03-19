<template>
  <form id="optionsForm" @submit.prevent="start">
    <img :src="image" v-if="image">
    <div>
      <div>
        <label for="file">
          Select an image
          <input type="file"
            id="file"
            accept="image/gif, image/jpeg, image/png"
            @change="fileChanged">
        </label>
        Board size:
        <input type="number" name="width" min="2" max="10" v-model.number="size.horizontal">
        ×
        <input type="number" name="height" min="2" max="10" v-model.number="size.vertical">
      </div>
      <button v-if="image">Start</button>
    </div>
  </form>
</template>

<script>
export default {
  data () {
    return {
      image: null,
      size: {
        horizontal: 3,
        vertical: 3
      }
    }
  },

  methods: {
    fileChanged (e) {
      if (!e.target.files.length) {
        this.image = null
        return
      }

      // Read the image into a data URL to use throughout the app.
      const reader = new FileReader()
      reader.onload = e => {
        this.image = e.target.result
      }
      reader.readAsDataURL(e.target.files[0])
    },

    /**
     * Start the game by emitting the event.
     */
    start () {
      this.$emit('gameStart', {
        image: this.image,
        size: this.size
      })
    },

    /**
     * Reset the options.
     */
    reset () {
      this.image = null
      document.querySelector('#optionsForm').reset()
    }
  }
}
</script>

<style lang="scss" scoped>
img {
  border: 1px solid #ccc;
  margin-bottom: 8px;
}

label[for=file] {
  color: #368ba0;
  cursor: pointer;
  display: inline-block;
  margin-right: 12px;
}

input[type=number] {
  height: 24px;
  font-size: 14px;
  border: 1px solid #ccc;
}

input[type=file] {
  display: none;
}

button {
  -webkit-appearance: none;
  padding: 6px 12px;
  background: #1ca76a;
  color: #fff;
  border-radius: 3px;
  border: 0;
  font-size: 14px;
  cursor: pointer;
  margin-top: 10px;
}
</style>
