<template>
  <h1>Color Guess</h1>
  <button v-if="!hasStarted" @click="startGame">new colors</button>
  <ColorOptions v-else :colorList="colorList" @answer="newColors" />
</template>

<script>
import ColorOptions from './components/ColorOptions.vue'

export default {
  name: 'App',
  components: {
    ColorOptions,
  },
  data() {
    return {
      colorList: [],
      hasStarted: false
    }
  },
  methods: {
    colorValue() {
      return Math.floor(Math.random() * 256)
    },
    generateColorList() {
      const { colorValue } = this
      for (let i = 0; i < 4; i++) {
        const color = `rgb(${colorValue()}, ${colorValue()}, ${colorValue()})`
        this.colorList[i] = color
      }
      console.log(this.colorList)
    },
    startGame() {
      this.generateColorList()
      this.hasStarted = true
    },
    newColors() {
      this.generateColorList()
    }
  },
}
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 3.75rem;
  }
</style>
