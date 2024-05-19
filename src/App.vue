<script setup>
import { ref, computed, onMounted } from 'vue';
import { useToast } from 'vue-toastification';

import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import Outlay from './components/Outlay.vue';
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

const toast = useToast();
const transactions = ref([]);

onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem('transactions'));

  if (savedTransactions) {
    transactions.value = savedTransactions;
  };
});

const total = computed(() => {
 return transactions.value.reduce((acc, transaction) => {
  return acc + transaction.amount;
 }, 0).toFixed(2);
});

const income = computed(() => {
 return transactions.value
 .filter((transaction) => transaction.amount > 0)
 .reduce((acc, transaction) => {
  return acc + transaction.amount;
 }, 0).toFixed(2);
});

const expense = computed(() => {
 return transactions.value
 .filter((transaction) => transaction.amount < 0)
 .reduce((acc, transaction) => {
  return acc + transaction.amount;
 }, 0).toFixed(2);
});

const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: generateUniqueId(),
    name: transactionData.name,
    amount: transactionData.amount
  });
  
  saveTransactionToLocalStorage();
  toast.success('Transaction is added.');
};

const generateUniqueId = () => {
  return Math.floor(Math.random() * 1000000)
};

const handleTransactionRemoved = (id) => {
  transactions.value = transactions.value.filter((transactions) => transactions.id !== id);
  saveTransactionToLocalStorage();
  toast.success('Transaction is removed.');
};

const saveTransactionToLocalStorage = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value));
};
</script>

<template>
  <div class="w-11/12 sm:w-96 grid gap-y-5 my-5 mx-auto">
    <Header />
    <Balance :total="+total" />
    <Outlay :income="+income" :expense="+expense" />
    <TransactionList @transactionRemoved="handleTransactionRemoved" :transactions="transactions" />
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
  </div>
</template>

