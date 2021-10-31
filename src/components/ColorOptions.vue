<template>
  <div v-if="results.length < 5">
    <h2>{{ correctColor }}</h2>
    <div class="color-options">
      <Color v-for="curColor in colorList" :key="curColor" :color="curColor" @click="checkAnswer" />
    </div>
    <Points :results="results"/>
  </div>
  <div v-else>
    <h2>Você acertou {{ results.reduce((acc, cur) => acc + cur, 0) }}/5</h2>
    <Points :results="results"/>
    <button @click="restartGame">RESTART</button>
  </div>
</template>

<script>
import Color from './Color.vue'
import Points from './Points.vue'

export default {
  components: {
    Color,
    Points,
  },
  props: ['colorList'],
  emits: ['answer'], // https://stackoverflow.com/a/64220977
  data() {
    return {
      correctColor: null,
      correctAnswer: null,
      results: [],
    }
  },
  mounted() {
    this.correctColor = this.colorList[Math.floor(Math.random() * this.colorList.length)]
      .match(/\d{1,3},\s?\d{1,3},\s?\d{1,3}/)[0]
  },
  methods: {
    newColors() {
      this.$emit('answer')
      this.correctColor = this.colorList[Math.floor(Math.random() * this.colorList.length)]
        .match(/\d{1,3},\s?\d{1,3},\s?\d{1,3}/)[0]
    },
    checkAnswer(e) {
      const chosenColor = e.target.style.cssText.match(/\d{1,3},\s?\d{1,3},\s?\d{1,3}/)[0]
      this.correctAnswer = chosenColor === this.correctColor
      this.correctAnswer ? this.results.push(1) : this.results.push(0)
      this.newColors()
    },
    restartGame() {
      this.results = []
      this.newColors()
    }
  }
}
</script>

<style>
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