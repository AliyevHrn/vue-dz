<script setup>
import { ref } from "vue";

// const emit = defineEmits(["cardReverse", "statusChange"]);
// function reverseCard() {
//   emit("cardReverse");
// }
// function changeStatus() {
//   emit("statusChange");
// }

const cardData = ref({
  word: "unadmitted",
  translation: "не допущенный",
  state: "closed",
  status: null,
});
</script>

<template>
  <div class="card">
    <div class="card-wrapper">
      <span class="card-number">01</span>
      <span class="card-en-text">{{ cardData.word }}</span>
      <span class="card-ru-text">{{ cardData.translation }}</span>
      <span class="card-reverse-text">Перевернуть</span>
    </div>
  </div>
</template>

<style scoped>
.card {
  width: 275px;
  height: 376px;
  border-radius: 16px;
  background-color: var(--color-white);
  padding: 28px 19px;
  cursor: pointer;
}
.card-wrapper {
  position: relative;
  height: 100%;
  border-radius: 16px;
  border: 1px solid var(--color-lightblue);
}
.card-number {
  position: absolute;
  left: 16px;
  font-size: 14px;
  font-weight: 400;
  top: -10px;
  padding: 1px;
  background: var(--color-white);
}
.card-en-text,
.card-ru-text {
  font-size: 18px;
  font-weight: 400;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.card-reverse-text {
  font-size: 12px;
  font-weight: 700;
  line-height: 18px;
  letter-spacing: 12%;
  position: absolute;
  bottom: -10px;
  left: 50%;
  padding: 1px;
  background: var(--color-white);
  text-transform: uppercase;
  transform: translateX(-50%);
}
</style>
