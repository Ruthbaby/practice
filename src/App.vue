<template>
  <Header />
  <div class="container">
    <Balance :total="total" />
    <IncomeExpenses :income="income" :expenses="expenses" />
    <TransactionList :transactions="transactions" />
    <AddTransaction />
  </div>
</template>

<script setup>
import Header from '@/components/Header.vue';
import Balance from '@/components/Balance.vue';
import IncomeExpenses from '@/components/IncomeExpenses.vue';
import TransactionList from '@/components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

import { ref, computed } from 'vue';
const transactions = ref([
  {id: 1, text: 'Flower', amount: -12.99},
  {id: 2, text: 'Salary', amount: 459.99},
  {id: 3, text: 'Block', amount: -52.39},
  {id: 4, text: 'SmartPhone', amount: 210},
  {id: 5, text: 'Services', amount: 130},
  ]);
  // console.log(transactions.value);
// To Get total
  const total = computed(() => {
    return transactions.value.reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0)
  })

  // To Get Income
  const income = computed(() => {
    return transactions.value.filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0).toFixed(2);
  })

  // To Get Expenses
  const expenses = computed(() => {
    return transactions.value.filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0).toFixed(2);
  })
</script>