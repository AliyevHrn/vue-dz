<script setup></script>

<template>
  <button class="button"><slot /></button>
</template>

<style scoped>
.button {
  font-size: 24px;
  font-weight: 400;
  padding: 16px 10px;
  border-radius: 30px;
  width: 315px;
  border: none;
  color: var(--color-white);
  background-color: var(--color-blue);
  cursor: pointer;
}
@media (max-width: 540px) {
  .button {
    font-size: 18px;
    width: 280px;
    padding: 12px 10px;
  }
}
</style>
