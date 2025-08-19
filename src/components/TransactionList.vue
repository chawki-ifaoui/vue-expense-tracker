<template>
  <div>
    <v-card-title class="text-h6 text-md-h5 font-weight-bold mb-3 mb-md-4">
      <v-icon icon="mdi-history" class="me-2"></v-icon>
      Transaction History
    </v-card-title>
    
    <!-- Date Filter -->
    <v-row class="mb-4">
      <v-col cols="12" sm="6">
        <v-select
          v-model="dateFilter"
          :items="dateFilterOptions"
          label="Filter by Date"
          variant="outlined"
          density="compact"
          prepend-inner-icon="mdi-filter"
          @update:model-value="applyDateFilter"
        ></v-select>
      </v-col>
      <v-col cols="12" sm="6" v-if="dateFilter === 'custom'">
        <v-text-field
          v-model="customDateRange"
          label="Custom Date Range"
          placeholder="e.g., Last 30 days"
          variant="outlined"
          density="compact"
          prepend-inner-icon="mdi-calendar-range"
          @keyup.enter="applyCustomDateFilter"
        ></v-text-field>
      </v-col>
    </v-row>
    
    <v-list class="pa-0">
      <v-list-item
        v-for="transaction in filteredAndSortedTransactions"
        :key="transaction.id"
        class="mb-2 rounded-lg"
        :class="transaction.amount < 0 ? 'bg-red-lighten-5' : 'bg-green-lighten-5'"
      >
        <template v-slot:prepend>
          <v-avatar
            :color="transaction.amount < 0 ? 'error' : 'success'"
            size="32"
            size-md="40"
          >
            <v-icon
              :icon="transaction.amount < 0 ? 'mdi-minus' : 'mdi-plus'"
              color="white"
              size="16"
              size-md="20"
            ></v-icon>
          </v-avatar>
        </template>
        
        <v-list-item-title class="font-weight-medium text-body-2 text-md-body-1">
          {{ transaction.text }}
        </v-list-item-title>
        
        <v-list-item-subtitle class="text-caption text-grey-600">
          <v-icon icon="mdi-calendar" size="12" class="me-1"></v-icon>
          {{ formatTransactionDate(transaction.date) }}
        </v-list-item-subtitle>
        
        <template v-slot:append>
          <div class="d-flex align-center">
            <span
              class="text-body-1 text-md-h6 font-weight-bold me-2 me-md-3"
              :class="transaction.amount < 0 ? 'text-error' : 'text-success'"
            >
              {{ transaction.amount < 0 ? '-' : '+' }}${{ Math.abs(transaction.amount).toFixed(2) }}
            </span>
            <v-btn
              icon="mdi-delete"
              variant="text"
              color="error"
              size="small"
              size-md="default"
              @click="deleteTransaction(transaction.id)"
            ></v-btn>
          </div>
        </template>
      </v-list-item>
    </v-list>
    
    <v-alert
      v-if="filteredAndSortedTransactions.length === 0"
      type="info"
      variant="tonal"
      class="mt-4"
    >
      {{ transactions.length === 0 ? 'No transactions yet. Add your first transaction below!' : 'No transactions found for the selected date range.' }}
    </v-alert>
  </div>
</template>

<script setup>
import { defineProps, computed, ref } from 'vue';

const props = defineProps({
  transactions: {
    type: Array,
    required: true,
  },
});

const emit = defineEmits(['transactionDeleted']);

const dateFilter = ref('all');
const customDateRange = ref('');

const dateFilterOptions = [
  { title: 'All Time', value: 'all' },
  { title: 'Today', value: 'today' },
  { title: 'Yesterday', value: 'yesterday' },
  { title: 'This Week', value: 'thisWeek' },
  { title: 'This Month', value: 'thisMonth' },
  { title: 'Last 30 Days', value: 'last30Days' },
  { title: 'Custom Range', value: 'custom' }
];

const deleteTransaction = (id) => {
  emit('transactionDeleted', id);
};

const formatTransactionDate = (dateString) => {
  if (!dateString) return '';
  
  const date = new Date(dateString);
  const today = new Date();
  const yesterday = new Date(today);
  yesterday.setDate(yesterday.getDate() - 1);
  
  // Check if it's today
  if (date.toDateString() === today.toDateString()) {
    return 'Today';
  }
  
  // Check if it's yesterday
  if (date.toDateString() === yesterday.toDateString()) {
    return 'Yesterday';
  }
  
  // Check if it's within the last 7 days
  const diffTime = Math.abs(today - date);
  const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));
  
  if (diffDays <= 7) {
    return date.toLocaleDateString('en-US', { weekday: 'long' });
  }
  
  // For older dates, show the full date
  return date.toLocaleDateString('en-US', {
    month: 'short',
    day: 'numeric',
    year: date.getFullYear() !== today.getFullYear() ? 'numeric' : undefined
  });
};

const applyDateFilter = () => {
  if (dateFilter.value === 'custom') {
    applyCustomDateFilter();
  }
};

const applyCustomDateFilter = () => {
  // This would implement custom date range filtering
  // For now, it just resets to all
  dateFilter.value = 'all';
};

const isTransactionInDateRange = (transaction) => {
  if (!transaction.date) return true;
  
  const transactionDate = new Date(transaction.date);
  const today = new Date();
  const startOfDay = new Date(today.getFullYear(), today.getMonth(), today.getDate());
  const endOfDay = new Date(today.getFullYear(), today.getMonth(), today.getDate(), 23, 59, 59);
  
  switch (dateFilter.value) {
    case 'today':
      return transactionDate >= startOfDay && transactionDate <= endOfDay;
    
    case 'yesterday':
      const yesterday = new Date(today);
      yesterday.setDate(yesterday.getDate() - 1);
      const startOfYesterday = new Date(yesterday.getFullYear(), yesterday.getMonth(), yesterday.getDate());
      const endOfYesterday = new Date(yesterday.getFullYear(), yesterday.getMonth(), yesterday.getDate(), 23, 59, 59);
      return transactionDate >= startOfYesterday && transactionDate <= endOfYesterday;
    
    case 'thisWeek':
      const startOfWeek = new Date(today);
      startOfWeek.setDate(today.getDate() - today.getDay());
      startOfWeek.setHours(0, 0, 0, 0);
      return transactionDate >= startOfWeek;
    
    case 'thisMonth':
      const startOfMonth = new Date(today.getFullYear(), today.getMonth(), 1);
      return transactionDate >= startOfMonth;
    
    case 'last30Days':
      const thirtyDaysAgo = new Date(today);
      thirtyDaysAgo.setDate(today.getDate() - 30);
      return transactionDate >= thirtyDaysAgo;
    
    default:
      return true;
  }
};

// Filter and sort transactions by date (newest first)
const filteredAndSortedTransactions = computed(() => {
  const filtered = props.transactions.filter(isTransactionInDateRange);
  return filtered.sort((a, b) => {
    const dateA = new Date(a.date || 0);
    const dateB = new Date(b.date || 0);
    return dateB - dateA;
  });
});
</script>
