<script setup>
import Fail from "@/icons/Fail.vue";
import Success from "@/icons/success.vue";
import { ref } from "vue";

const emit = defineEmits(["fail-card", "success-card"]);
function handleSuccess() {
  emit("success-card", {
    id: props.id,
    status: "success",
  });
}
function handleFail() {
  emit("fail-card", {
    id: props.id,
    status: "fail",
  });
}

const props = defineProps({
  id: Number,
  word: String,
  translation: String,
  status: "closed" | "pending" | "success" | "fail",
});
</script>

<template>
  <div
    class="card"
    :class="{
      closed: status === 'closed',
      pending: status === 'pending',
      success: status === 'success',
      fail: status === 'fail',
    }"
  >
    <div class="card-wrapper">
      <span class="card-id">{{ id < 10 ? "0" : "" }}{{ id }}</span>
      <span class="card-correct-icon" v-show="status === 'success'">
        <Success />
      </span>
      <span class="card-fail-icon" v-show="status === 'fail'">
        <Fail />
      </span>
      <span v-show="status === 'closed'" class="card-word">
        {{ word }}
      </span>
      <span
        v-show="
          status === 'pending' || status === 'success' || status === 'fail'
        "
        class="card-translation"
        >{{ translation }}</span
      >
      <span class="card-status" v-show="status === 'closed'">Перевернуть</span>
      <span
        class="card-status"
        v-show="status === 'success' || status === 'fail'"
        >Завершено</span
      >
      <div class="card-status" v-show="status === 'pending'">
        <button @click="handleFail">
          <Fail />
        </button>
        <button @click="handleSuccess">
          <Success />
        </button>
      </div>
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
</style>
