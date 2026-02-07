<script setup>
import { ref, onMounted } from "vue";
import Button from "./components/Button.vue";
import Card from "./components/Card.vue";
import Header from "./components/Header.vue";

const ENDPOINT = "http://localhost:8080/api/random-words";
const data = ref(null);
const gameIsStarted = ref(false);
const scoreNumber = ref(0);

const fetchData = async () => {
  try {
    const response = await fetch(ENDPOINT);
    if (!response.ok) {
      throw new Error("Проблемы с запросом к api");
    }
    data.value = await response.json();
  } catch (err) {
    console.log(err.message);
  }
};

onMounted(() => {
  fetchData();
});

function resetGame() {
  fetchData();
  scoreNumber.value = 0;
  gameIsStarted.value = true;
}
function startGame() {
  gameIsStarted.value = true;
}
function handleStatus(status) {
  status === "success" ? (scoreNumber.value += 1) : scoreNumber.value;
}
</script>

<template>
  <Header :score-number="scoreNumber" />
  <div class="card-list" v-if="gameIsStarted">
    <Card
      v-for="(card, i) in data"
      :key="card.word"
      :id="i + 1"
      :word="card.word"
      :translation="card.translation"
      @fail-status="handleStatus"
      @success-status="handleStatus"
    />
  </div>
  <div class="btns-list">
    <Button class="btn-start" @click="startGame()" v-if="!gameIsStarted"
      >Начать игру</Button
    >
    <Button class="btn-reset" @click="resetGame()" v-if="gameIsStarted"
      >Начать заново</Button
    >
  </div>
</template>

<style scoped>
.card-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  gap: 100px;
}
.btns-list {
  display: flex;
  justify-content: center;
}
.btn-start {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.btn-reset {
  margin-top: 50px;
}
@media (max-width: 1440px) {
  .card-list {
    gap: 50px;
  }
}
@media (max-width: 1200px) {
  .card-list {
    gap: 30px;
  }
}
@media (max-width: 1024px) {
  .card-list {
    gap: 20px;
  }
}
@media (max-width: 840px) {
  .card-list {
    gap: 10px;
  }
}
</style>
