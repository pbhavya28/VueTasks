<script setup>
import { computed } from 'vue';

const emit = defineEmits(['reset']);

const props = defineProps(['group', 'total', 'payers']);

const perPerson = computed(() => props.total / props.group.length);

const balances = computed(() => {
  const map = {};
  props.group.forEach(member => {
    map[member.name] = -perPerson.value;
  });
  props.payers.forEach(payer => {
    if (payer.name) {
      map[payer.name] += payer.paid;
    }
  });
  return map;
});

const transactions = computed(() => {
  const debtors = [];
  const creditors = [];

  for (const [name, balance] of Object.entries(balances.value)) {
    if (balance < 0) debtors.push({ name, amount: -balance });
    if (balance > 0) creditors.push({ name, amount: balance });
  }

  const result = [];

  while (debtors.length && creditors.length) {
    const debtor = debtors[0];
    const creditor = creditors[0];

    const minAmount = Math.min(debtor.amount, creditor.amount);

    result.push(`${debtor.name} owes ₹${minAmount.toFixed(2)} to ${creditor.name}`);

    debtor.amount -= minAmount;
    creditor.amount -= minAmount;

    if (debtor.amount === 0) debtors.shift();
    if (creditor.amount === 0) creditors.shift();
  }

  return result;
});

function planNextOuting() {
  emit('reset');
}
</script>

<template>
  <div class="container mt-5">

    <div class="bg-primary text-white text-center py-3 rounded-top shadow-sm">
      <h2 class="mb-0">Summary</h2>
      <p class="mb-0 small">Who owes whom, and how much</p>
    </div>

    <div class="card shadow border-0 rounded-bottom">
      <div class="card-body bg-light">

        <p><strong>Total Expense:</strong> ₹{{ props.total }}</p>
        <p><strong>Per Person Share:</strong> ₹{{ perPerson.toFixed(2) }}</p>

        <h5 class="mt-4 mb-2 text-secondary">Payments</h5>
        <ul class="list-group mb-3">
          <li class="list-group-item" v-for="payer in props.payers" :key="payer.name">
            {{ payer.name }} paid ₹{{ payer.paid }}
          </li>
        </ul>

        <h5 class="mb-2 text-secondary">Balances</h5>
        <ul class="list-group mb-3">
          <li class="list-group-item" v-for="(bal, name) in balances" :key="name">
            {{ name }}: {{ bal >= 0 ? '+' : '' }}₹{{ bal.toFixed(2) }}
          </li>
        </ul>

        <h5 class="mb-2 text-secondary">Who Owes Whom</h5>
        <ul class="list-group mb-4">
          <li class="list-group-item" v-for="(txn, index) in transactions" :key="index">
            {{ txn }}
          </li>
        </ul>

        <button
          @click="planNextOuting"
          class="btn btn-primary w-100"
        >
          Plan Next Outing
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
</style>
