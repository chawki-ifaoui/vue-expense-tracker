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
        class="mb-3 mb-md-4"
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
      
      <v-text-field
        v-model="date"
        label="Date"
        placeholder="Select date..."
        variant="outlined"
        prepend-inner-icon="mdi-calendar"
        :rules="[v => !!v || 'Date is required']"
        class="mb-4 mb-md-6"
        density="compact"
        density-md="default"
        readonly
        @click="showDatePicker = true"
      ></v-text-field>
      
      <v-dialog v-model="showDatePicker" max-width="400">
        <v-card>
          <v-card-title class="text-h6">
            Select Transaction Date
          </v-card-title>
          <v-card-text>
            <v-date-picker
              v-model="selectedDate"
              @update:model-value="onDateSelected"
              :max="new Date().toISOString().substr(0, 10)"
            ></v-date-picker>
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn
              color="primary"
              @click="showDatePicker = false"
            >
              OK
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
      
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
import { ref, onMounted } from 'vue';

const text = ref('');
const amount = ref('');
const date = ref('');
const selectedDate = ref('');
const showDatePicker = ref(false);
const loading = ref(false);
const form = ref(null);

// Get toast interface
const toast = useToast();

const emit = defineEmits(['transactionSubmitted']);

// Set default date to today
onMounted(() => {
  const today = new Date().toISOString().substr(0, 10);
  selectedDate.value = today;
  date.value = formatDateForDisplay(today);
});

const formatDateForDisplay = (dateString) => {
  const date = new Date(dateString);
  return date.toLocaleDateString('en-US', {
    year: 'numeric',
    month: 'long',
    day: 'numeric'
  });
};

const onDateSelected = (newDate) => {
  if (newDate) {
    date.value = formatDateForDisplay(newDate);
    showDatePicker.value = false;
  }
};

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
    date: selectedDate.value,
    displayDate: date.value
  };

  emit('transactionSubmitted', transactionData);

  // Clear form fields
  text.value = '';
  amount.value = '';
  selectedDate.value = new Date().toISOString().substr(0, 10);
  date.value = formatDateForDisplay(selectedDate.value);
  form.value.resetValidation();
  
  loading.value = false;
};
</script>
