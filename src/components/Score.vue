<script setup>
import ScoreIcon from "@/icons/ScoreIcon.vue";
import { ref } from "vue";

const scoreNumber = ref(0);
</script>

<template>
  <div class="score">
    <span class="score-number">{{ scoreNumber }}</span>
    <ScoreIcon />
  </div>
</template>

<style scoped>
.score {
  display: flex;
  align-items: center;
  gap: 10px;
  background: var(--color-lightblue);
  padding: 12px 24px;
  border-radius: 30px;
}
.score-number {
  color: var(--color-blue);
}
</style>
