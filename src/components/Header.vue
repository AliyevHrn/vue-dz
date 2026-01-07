<script setup>
import Score from "./Score.vue";
</script>
<template>
  <div class="header">
    <h1>Запомни слово</h1>
    <Score />
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
  letter-spacing: 12%;
  transform: scaleY(0.8);
  text-transform: uppercase;
}
</style>
