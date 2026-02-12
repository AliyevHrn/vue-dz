<script setup>
import Fail from "@/icons/Fail.vue";
import Success from "@/icons/Success.vue";
import { ref } from "vue";

const cardStatus = ref("closed");
const props = defineProps({
  id: Number,
  word: String,
  translation: String,
});
const emit = defineEmits(["successStatus", "failStatus"]);
function successStatus() {
  cardStatus.value = "success";
  emit("successStatus", cardStatus.value);
}
function failStatus() {
  cardStatus.value = "fail";
  emit("failStatus", cardStatus.value);
}
</script>

<template>
  <div
    class="card"
    :class="{
      closed: cardStatus === 'closed',
      pending: cardStatus === 'pending',
      success: cardStatus === 'success',
      fail: cardStatus === 'fail',
    }"
    @click.once="cardStatus = 'pending'"
  >
    <div class="card-wrapper">
      <span class="card-id">{{ id < 10 ? "0" : "" }}{{ id }}</span>
      <span class="card-correct-icon" v-show="cardStatus === 'success'">
        <Success />
      </span>
      <span class="card-fail-icon" v-show="cardStatus === 'fail'">
        <Fail />
      </span>
      <span v-show="cardStatus === 'closed'" class="card-word">
        {{ word }}
      </span>
      <span
        v-show="
          cardStatus === 'pending' ||
          cardStatus === 'success' ||
          cardStatus === 'fail'
        "
        class="card-translation"
        >{{ translation }}</span
      >
      <span class="card-status" v-show="cardStatus === 'closed'"
        >Перевернуть</span
      >
      <span
        class="card-status"
        v-show="cardStatus === 'success' || cardStatus === 'fail'"
        >Завершено</span
      >
      <div class="card-status" v-show="cardStatus === 'pending'">
        <button @click="failStatus">
          <Fail />
        </button>
        <button @click="successStatus">
          <Success />
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card {
  height: 376px;
  border-radius: 16px;
  background-color: var(--color-white);
  padding: 28px 20px;
  cursor: pointer;
}
.card-wrapper {
  position: relative;
  height: 100%;
  border-radius: 16px;
  border: 1px solid var(--color-lightblue);
}
.card-id {
  position: absolute;
  left: 16px;
  font-size: 14px;
  font-weight: 400;
  top: -10px;
  padding: 1px;
  background: var(--color-white);
}
.card-correct-icon,
.card-fail-icon {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
}
.card-correct-icon {
  top: -15px;
}
.card-fail-icon {
  top: -20px;
}
.card-word,
.card-translation {
  font-size: 18px;
  font-weight: 400;
  text-align: center;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.card-status {
  font-size: 12px;
  font-weight: 600;
  line-height: 18px;
  letter-spacing: 0.1rem;
  position: absolute;
  bottom: -10px;
  left: 50%;
  padding: 1px;
  background: var(--color-white);
  text-transform: uppercase;
  transform: translateX(-50%);
}
.card.pending .card-status {
  display: flex;
  justify-content: space-between;
  width: 100px;
  bottom: -15px;
  padding: 0 10px;
}
.card-status button {
  background-color: transparent;
  border: none;
  cursor: pointer;
}
.card-status button svg {
  width: 24px;
  height: 24px;
}
@media (max-width: 540px) {
  .card {
    height: 280px;
    padding: 20px 12px;
  }
  .card-correct-icon,
  .card-fail-icon {
    top: -12px;
  }
  .card-correct-icon svg,
  .card-fail-icon svg {
    width: 24px;
    height: 24px;
  }
  .card-word,
  .card-translation {
    font-size: 16px;
  }
  .card-status {
    font-size: 10px;
  }
}
@media (max-width: 420px) {
  .card {
    height: 240px;
  }
  .card-word,
  .card-translation {
    font-size: 14px;
  }
}
</style>
