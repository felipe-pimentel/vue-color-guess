<template>
  <div class="points">
    <div
      class="point"
      v-for="result in results"
      :class="{ error: result === 0, correct: result !== 0 }"
      :key="result"
    >
    </div>
  </div>
</template>

<script>
export default {
  props: ['results'],
}
</script>

<style>
  .points {
    display: grid;
    gap: 0.5rem;
    grid-template-columns: repeat(5, 1fr);
    margin: 1rem auto;
    width: 12rem;
  }
  .point {
    aspect-ratio: 1;
    border-radius: 50%;
  }
  .correct {
    background: green;
  }
  .error {
    background: red;
  }
</style>