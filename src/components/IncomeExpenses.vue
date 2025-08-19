<template>
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
});
</script>
