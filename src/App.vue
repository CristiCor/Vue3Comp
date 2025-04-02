<template>
  <Header />
  <div class="container">
      <Balance :total="+total"/>
      <IncomeExpences :income="+income" :expenses="+expenses"/>
      <TranzactionList :transactions="transactions" @transactionDeleted="handleTransactionDeleted"/>
      <AddTransaction @transactionSubmitted="handleTransactionSubmitted"/>
  </div>
</template>

<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpences from './components/IncomeExpense.vue';
import TranzactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

import {useToast} from 'vue-toastification';

import {ref, computed } from 'vue';

const toast = useToast();

const transactions = ref([
    {id:1, text: "Flower", amount: parseFloat("-19.00")},
    {id:2, text: "Salary", amount: parseFloat("1000.00")},
    {id:3, text: "Book", amount: parseFloat("-10.00")},
    {id:4, text: "Revenue", amount: parseFloat("8000.00")},
]);

//Get total
const total = computed(()=>{
  return transactions.value.reduce((acc, transaction)=> acc + transaction.amount, 0);
});

//get Income
const income = computed(()=>{
  return transactions.value
  .filter((transaction)=> transaction.amount > 0 )
  .reduce((acc, transaction) => acc + transaction.amount, 0)
  .toFixed(2);
});

//get expenses
const expenses = computed(()=>{
  return transactions.value
    .filter((transaction) => transaction.amount < 0 )
    .reduce((acc, transaction) => acc + transaction.amount, 0)
    .toFixed(2);
});

//Add transaction
const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: generateUniqueId(),
    text: transactionData.text,
    amount: transactionData.amount
  });

  toast.success('Transaction added !');
};

const generateUniqueId = () => {
  return Math.floor(Math.random() * 1000000);
};

//Delete transaction
const handleTransactionDeleted = (id) => {
  transactions.value = transactions.value.filter((transaction) => transaction.id !== id);

  toast.success('Transaction deleted !');
}

</script>