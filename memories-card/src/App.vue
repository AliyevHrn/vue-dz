<script setup>
const curDate = new Date();
</script>

<template>
  <div>{{ curDate.toLocaleString() }}</div>
</template>

<style scoped></style>
