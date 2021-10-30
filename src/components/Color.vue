<template>
  <div class="color">
    {{ color }}
  </div>
</template>

<script>
export default {
  props: ['color'],
}
</script>

<style scoped>
  .color {
    background: v-bind(color);
  }
</style>