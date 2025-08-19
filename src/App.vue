<template>
  <v-app>
    <Header />
    <v-main class="bg-grey-lighten-4">
      <v-container class="py-4 py-md-8 px-4">
        <v-row justify="center">
          <v-col cols="12" sm="10" md="8" lg="6">
            <v-card class="pa-4 pa-md-6" elevation="3">
              <Balance :total="total" />
              <v-divider class="my-4 my-md-6"></v-divider>
              <IncomeExpenses 
                :income="+income" 
                :expenses="+expenses" 
                :transactions="transactions"
              />
              <v-divider class="my-4 my-md-6"></v-divider>
              <TransactionList
                :transactions="transactions"
                @transactionDeleted="handleTransactionDeleted"
              />
              <v-divider class="my-4 my-md-6"></v-divider>
              <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpenses from './components/IncomeExpenses.vue';
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

import { ref, computed, onMounted } from 'vue';

import { useToast } from 'vue-toastification';

const toast = useToast();

const transactions = ref([]);

onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem('transactions'));

  if (savedTransactions) {
    // Add date field to existing transactions if they don't have it
    transactions.value = savedTransactions.map(transaction => ({
      ...transaction,
      date: transaction.date || new Date().toISOString().substr(0, 10),
      displayDate: transaction.displayDate || new Date().toLocaleDateString('en-US', {
        year: 'numeric',
        month: 'long',
        day: 'numeric'
      })
    }));
  }
});

// Get total
const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0);
});

// Get income
const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => acc + transaction.amount, 0)
    .toFixed(2);
});

// Get expenses
const expenses = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => acc + transaction.amount, 0)
    .toFixed(2);
});

// Submit transaction
const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: generateUniqueId(),
    text: transactionData.text,
    amount: transactionData.amount,
    date: transactionData.date,
    displayDate: transactionData.displayDate,
  });

  saveTransactionsToLocalStorage();

  toast.success('Transaction added.');
};

// Generate unique ID
const generateUniqueId = () => {
  return Math.floor(Math.random() * 1000000);
};

// Delete transaction
const handleTransactionDeleted = (id) => {
  transactions.value = transactions.value.filter(
    (transaction) => transaction.id !== id
  );

  saveTransactionsToLocalStorage();

  toast.success('Transaction deleted.');
};

// Save transactions to local storage
const saveTransactionsToLocalStorage = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value));
};
</script>
