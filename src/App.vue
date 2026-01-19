<script setup>
import { ref } from "vue";
import Button from "./components/Button.vue";
import Card from "./components/Card.vue";
import Header from "./components/Header.vue";

const gameStatus = ref(false);
let scoreNumber = ref(0);
const wordsList = ref([
  {
    id: 1,
    word: "table",
    tranlation: "Стол",
    status: "closed",
  },
  {
    id: 2,
    word: "pen",
    tranlation: "Ручка",
    status: "closed",
  },
  {
    id: 3,
    word: "task",
    tranlation: "Задача",
    status: "closed",
  },
  {
    id: 4,
    word: "book",
    tranlation: "Книга",
    status: "closed",
  },
]);

function openCard(card) {
  card.status = "pending";
}
function updateStatus({ id, status }) {
  const cardIndex = wordsList.value.findIndex((card) => card.id === id);
  wordsList.value[cardIndex].status = status;

  // Обновляем счет
  if (status === "success") {
    scoreNumber.value += 1;
  }
  // else if (status === "fail") {
  //   scoreNumber.value = Math.max(0, scoreNumber.value - 1);
  // }
}
function resetGame() {
  wordsList.value.forEach((card) => {
    card.status = "closed";
  });
  scoreNumber.value = 0;
  gameStatus.value = true;
}
function startGame() {
  gameStatus.value = true;
}
</script>

<template>
  <Header :score-number="scoreNumber" />
  <div class="card-list" v-if="gameStatus">
    <Card
      v-for="card in wordsList"
      :key="card.id"
      :id="card.id"
      :word="card.word"
      :translation="card.tranlation"
      :status="card.status"
      @click.capture="openCard(card)"
      @fail-card="updateStatus"
      @success-card="updateStatus"
    />
  </div>
  <div class="btns-list">
    <Button class="btn-start" @click="startGame()" v-if="!gameStatus"
      >Начать игру</Button
    >
    <Button class="btn-reset" @click="resetGame()" v-if="gameStatus"
      >Начать заново</Button
    >
  </div>
</template>

<style scoped>
.card-list {
  display: flex;
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
</style>
