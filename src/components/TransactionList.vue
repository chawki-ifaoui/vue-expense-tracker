<template>
  <div>
    <v-card-title class="text-h6 text-md-h5 font-weight-bold mb-3 mb-md-4">
      <v-icon icon="mdi-history" class="me-2"></v-icon>
      Transaction History
    </v-card-title>
    
    <v-list class="pa-0">
      <v-list-item
        v-for="transaction in transactions"
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
      v-if="transactions.length === 0"
      type="info"
      variant="tonal"
      class="mt-4"
    >
      No transactions yet. Add your first transaction below!
    </v-alert>
  </div>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  transactions: {
    type: Array,
    required: true,
  },
});

const emit = defineEmits(['transactionDeleted']);

const deleteTransaction = (id) => {
  emit('transactionDeleted', id);
};
</script>
