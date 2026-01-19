<script setup>
import Score from "./Score.vue";

defineProps({
  scoreNumber: {
    type: Number,
    default: 0,
  },
});
</script>
<template>
  <div class="header">
    <h1>Запомни слово</h1>
    <Score :score-number />
  </div>
</template>

<style scoped>
.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 85px;
}
h1 {
  font-size: 16px;
  font-weight: 700;
  line-height: 24px;
  letter-spacing: 0.1rem;
  transform: scaleY(0.8);
  text-transform: uppercase;
}
</style>
