<template>
  <Header />
  <div class="container">
      <Balance :total="total"/>
      <IncomeExpences />
      <TranzactionList :transactions="transactions"/>
      <AddTransaction />
  </div>
</template>

<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpences from './components/IncomeExpense.vue';
import TranzactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

import {ref, computed } from 'vue';

const transactions = ref([
    {id:1, text: "Flower", amount: -19.99},
    {id:2, text: "Salary", amount: 11333.99},
    {id:3, text: "Book", amount: -10.99},
    {id:4, text: "Revenue", amount: 22000.00},
]);

const total = computed(()=>{
  return transactions.value.reduce((acc, transaction)=> {
    return acc + transaction.amount; 
  }, 0);
});
</script>