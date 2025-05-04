<!-- Task Title: Let’s Do Dutch – Expense Splitter App
Objective: Use features of Vue.js and Tailwind / Bootstrap
 
Build a simple, clean 3-screen app to split shared expenses among friends or team members.
The app allows users to enter people, add expenses, and see who owes whom how much.
 
The app must have 3 screens at least
home screen : where you create a group and add, remove particpants / team members from the group
expense screen : add expences where the expences gets divided amongst each member equally.
select a payer ( a person who will collect the money and pays the bill )
on the day of expence lets say 2 out of 5 make the full payment, then the remaining 3 will have to pay to the 2 particpants who have paid.
-------------------------------------------------------------------------------------------
eg : lets say 5 member team visits a restaurant for snacks and the bill was 1500/-
the app then shows the per head contribution as 300/-
but lets say 2 people paid the restaurant bill on that day ( 1st person pays 1000/- and second person pays 500/- then the remaining 3 will have to pay 900/- which will be split between 2 people who have already paid. so the 1st person will get 700/- and 2nd person will get 200/-
summary screen : who owes whom -->


<script setup>
import { ref } from 'vue';
import HomeScreen from './components/HomeScreen.vue';
import ExpenseScreen from './components/ExpenseScreen.vue';
import SummaryScreen from './components/SummaryScreen.vue';

const currentScreen = ref('home');
const group = ref([]);
const expenseData = ref({
  total: 0,
  payers: []
});

function handleGroup(newGroup) {
  group.value = newGroup;
  currentScreen.value = 'expense';
}

function goToSummary(data) {
  expenseData.value = data;
  currentScreen.value = 'summary';
}

function resetApp() {
  group.value = [];
  expenseData.value = { total: 0, payers: [] };
  currentScreen.value = 'home';
}
</script>

<template>
  <div class="p-6">
    <HomeScreen v-if="currentScreen === 'home'" @groupCreated="handleGroup" />
    <ExpenseScreen
      v-if="currentScreen === 'expense'"
      :array="group"
      @goToSummary="goToSummary"
    />
    <SummaryScreen
      v-if="currentScreen === 'summary'"
      :group="group"
      :total="expenseData.total"
      :payers="expenseData.payers"
      @reset="resetApp"
    />
  </div>
</template>
