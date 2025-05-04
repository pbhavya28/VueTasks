<script setup>
import { ref, computed, watch } from 'vue';

const props = defineProps(['array']);
const emit = defineEmits(['goToSummary']);

const totalExpense = ref(2000);
const numberOfPayers = ref(0);
const payers = ref([]);

watch(numberOfPayers, (newVal) => {
  payers.value = Array.from({ length: newVal }, () => ({ name: '', paid: 0 }));
});

const perPersonShare = computed(() => {
  return props.array.length ? (totalExpense.value / props.array.length).toFixed(2) : 0;
});

function goToSummaryScreen() {
  emit('goToSummary', {
    total: totalExpense.value,
    payers: payers.value
  });
}
</script>

<template>
  <div class="container mt-5">
    <div class="bg-primary text-white text-center py-3 rounded-top shadow-sm">
      <h2 class="mb-0">Expense Entry</h2>
      <p class="mb-0 small">Total cost and who paid</p>
    </div>

    <div class="card shadow border-0 rounded-bottom">
      <div class="card-body bg-light">
        <div class="mb-4">
          <label class="form-label fw-semibold">Total Expense (₹)</label>
          <input type="number" min="0" v-model="totalExpense" class="form-control" />
        </div>

        <p class="fw-medium mb-3">Per Person Share: ₹{{ perPersonShare }}</p>

        <div class="mb-4">
          <label class="form-label fw-semibold">How many people paid?</label>
          <input
            type="number"
            min="1"
            :max="props.array.length"
            v-model.number="numberOfPayers"
            class="form-control"
          />
        </div>

        <div
          v-for="(payer, index) in payers"
          :key="index"
          class="mb-4 border rounded p-3 bg-white"
        >
          <label class="form-label">Payer {{ index + 1 }} Name</label>
          <select v-model="payer.name" class="form-select mb-2">
            <option value="" disabled>Select a person</option>
            <option v-for="person in props.array" :key="person.name" :value="person.name">
              {{ person.name }}
            </option>
          </select>

          <label class="form-label">Amount Paid</label>
          <input
            type="number"
            min="0"
            v-model.number="payer.paid"
            class="form-control"
            placeholder="₹ Paid"
          />
        </div>

        <button
          @click="goToSummaryScreen"
          class="btn btn-success w-100 mt-3"
        >
          Go to Summary
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
</style>
