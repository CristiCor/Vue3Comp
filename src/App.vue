<template>
  <Header />
  <div class="container">
      <Balance />
      <IncomeExpences />
      <TranzactionList />
      <AddTransaction />
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpences from './components/IncomeExpense.vue';
import TranzactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

export default {
  components:{
    Header,
    Balance,
    IncomeExpences,
    TranzactionList,
    AddTransaction
},

};
</script>