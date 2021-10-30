<template>
  <h1>Color Guess</h1>
  <button @click="generateColorList">new colors</button>
  <div class="color-options">
    <Color v-for="curColor in colorList" :key="curColor" :color="curColor"/>
  </div>
</template>

<script>
import Color from './components/Color.vue'

export default {
  name: 'App',
  components: {
    Color,
  },
  data() {
    return {
      colorList: [],
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
  },
  mounted() {
    this.generateColorList()
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
  .color-options {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr 1fr;
    height: 20rem;
    width: 20rem;
    gap: 0.5rem;
    margin: 2rem auto;
  }
</style>
