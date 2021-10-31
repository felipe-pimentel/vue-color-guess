<template>
  <h2>{{ correctColor }}</h2>
  <div class="color-options">
    <Color v-for="curColor in colorList" :key="curColor" :color="curColor" @click="checkAnswer" />
  </div>
  <h2 v-if="hasAnswered">
    <span v-if="correctAnswer">Você acertou!!! \o/</span>
    <span v-else>Ah, você errou... =(</span>
  </h2>
</template>

<script>
import Color from './Color.vue'

export default {
  components: {
    Color,
  },
  props: ['colorList'],
  emits: ['answer'], // https://stackoverflow.com/a/64220977
  data() {
    return {
      correctColor: null,
      hasAnswered: false,
      correctAnswer: null,
    }
  },
  mounted() {
    this.correctColor = this.colorList[Math.floor(Math.random() * this.colorList.length)]
      .match(/\d{1,3},\s?\d{1,3},\s?\d{1,3}/)[0]
  },
  methods: {
    newColors() {
      this.$emit('answer')
      this.hasAnswered = false
      this.correctColor = this.colorList[Math.floor(Math.random() * this.colorList.length)]
        .match(/\d{1,3},\s?\d{1,3},\s?\d{1,3}/)[0]
    },
    checkAnswer(e) {
      const chosenColor = e.target.style.cssText.match(/\d{1,3},\s?\d{1,3},\s?\d{1,3}/)[0]
      this.correctAnswer = chosenColor === this.correctColor
      this.hasAnswered = true
      setTimeout(() => this.newColors(), 2000)
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