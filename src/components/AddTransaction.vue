<template>
  <div>
    <v-card-title class="text-h6 text-md-h5 font-weight-bold mb-3 mb-md-4">
      <v-icon icon="mdi-plus-circle" class="me-2"></v-icon>
      Add New Transaction
    </v-card-title>
    
    <v-form @submit.prevent="onSubmit" ref="form">
      <v-text-field
        v-model="text"
        label="Transaction Description"
        placeholder="Enter transaction description..."
        variant="outlined"
        prepend-inner-icon="mdi-text"
        :rules="[v => !!v || 'Description is required']"
        class="mb-3 mb-md-4"
        density="compact"
        density-md="default"
      ></v-text-field>
      
      <v-text-field
        v-model="amount"
        label="Amount"
        placeholder="Enter amount..."
        variant="outlined"
        prepend-inner-icon="mdi-currency-usd"
        type="number"
        step="0.01"
        :rules="[
          v => !!v || 'Amount is required',
          v => !isNaN(v) || 'Amount must be a number',
          v => parseFloat(v) !== 0 || 'Amount cannot be zero'
        ]"
        class="mb-4 mb-md-6"
        density="compact"
        density-md="default"
      >
        <template v-slot:append>
          <v-tooltip location="top">
            <template v-slot:activator="{ props }">
              <v-icon
                v-bind="props"
                icon="mdi-information"
                color="info"
                size="small"
                size-md="default"
              ></v-icon>
            </template>
            <span>Positive for income, negative for expense</span>
          </v-tooltip>
        </template>
      </v-text-field>
      
      <v-btn
        type="submit"
        color="primary"
        size="large"
        size-md="x-large"
        block
        :loading="loading"
        prepend-icon="mdi-plus"
        class="text-body-1 text-md-h6"
      >
        Add Transaction
      </v-btn>
    </v-form>
  </div>
</template>

<script setup>
import { useToast } from 'vue-toastification';
import { ref } from 'vue';

const text = ref('');
const amount = ref('');
const loading = ref(false);
const form = ref(null);

// Get toast interface
const toast = useToast();

const emit = defineEmits(['transactionSubmitted']);

const onSubmit = async () => {
  loading.value = true;
  
  // Validate form
  const { valid } = await form.value.validate();
  
  if (!valid) {
    loading.value = false;
    toast.error('Please fill in all required fields correctly.');
    return;
  }

  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value),
  };

  emit('transactionSubmitted', transactionData);

  // Clear form fields
  text.value = '';
  amount.value = '';
  form.value.resetValidation();
  
  loading.value = false;
};
</script>
