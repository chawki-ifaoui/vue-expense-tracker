<template>
  <div>
    <v-row class="mb-3">
      <v-col cols="12">
        <v-card-subtitle class="text-caption text-grey-600 pa-0">
          <v-icon icon="mdi-calendar-range" size="14" class="me-1"></v-icon>
          {{ getDateRangeText() }}
        </v-card-subtitle>
      </v-col>
    </v-row>
    
    <v-row>
      <v-col cols="6">
        <v-card
          class="pa-3 pa-md-4 text-center"
          color="success"
          elevation="2"
        >
          <v-icon
            icon="mdi-trending-up"
            size="24"
            size-md="32"
            color="white"
            class="mb-2"
          ></v-icon>
          <v-card-title class="text-subtitle-2 text-md-h6 text-white font-weight-medium">
            INCOME
          </v-card-title>
          <v-card-text class="pa-0">
            <div class="text-h6 text-md-h5 font-weight-bold text-white">
              +${{ income.toFixed(2) }}
            </div>
          </v-card-text>
        </v-card>
      </v-col>
      <v-col cols="6">
        <v-card
          class="pa-3 pa-md-4 text-center"
          color="error"
          elevation="2"
        >
          <v-icon
            icon="mdi-trending-down"
            size="24"
            size-md="32"
            color="white"
            class="mb-2"
          ></v-icon>
          <v-card-title class="text-subtitle-2 text-md-h6 text-white font-weight-medium">
            EXPENSE
          </v-card-title>
          <v-card-text class="pa-0">
            <div class="text-h6 text-md-h5 font-weight-bold text-white">
              -${{ Math.abs(expenses).toFixed(2) }}
            </div>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  income: {
    type: Number,
    required: true,
  },
  expenses: {
    type: Number,
    required: true,
  },
  transactions: {
    type: Array,
    default: () => []
  }
});

const getDateRangeText = () => {
  if (!props.transactions || props.transactions.length === 0) {
    return 'All time';
  }
  
  const dates = props.transactions
    .filter(t => t.date)
    .map(t => new Date(t.date))
    .sort((a, b) => a - b);
  
  if (dates.length === 0) return 'All time';
  
  const oldest = dates[0];
  const newest = dates[dates.length - 1];
  const today = new Date();
  
  // If all transactions are from today
  if (oldest.toDateString() === today.toDateString() && 
      newest.toDateString() === today.toDateString()) {
    return 'Today';
  }
  
  // If all transactions are from this month
  if (oldest.getMonth() === today.getMonth() && 
      oldest.getFullYear() === today.getFullYear() &&
      newest.getMonth() === today.getMonth() && 
      newest.getFullYear() === today.getFullYear()) {
    return `This month (${today.toLocaleDateString('en-US', { month: 'long', year: 'numeric' })})`;
  }
  
  // If all transactions are from this year
  if (oldest.getFullYear() === today.getFullYear() && 
      newest.getFullYear() === today.getFullYear()) {
    return `This year (${today.getFullYear()})`;
  }
  
  // Show date range
  return `${oldest.toLocaleDateString('en-US', { month: 'short', year: 'numeric' })} - ${newest.toLocaleDateString('en-US', { month: 'short', year: 'numeric' })}`;
};
</script>
