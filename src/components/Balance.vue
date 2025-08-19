<template>
  <div class="text-center">
    <v-card
      class="pa-6 mb-4"
      color="primary"
      elevation="4"
    >
      <v-card-title class="text-h6 text-white font-weight-medium">
        YOUR BALANCE
      </v-card-title>
      <v-card-text class="pa-0">
        <div class="text-h3 font-weight-bold text-white">
          ${{ total.toFixed(2) }}
        </div>
      </v-card-text>
    </v-card>
  </div>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  total: {
    type: Number,
    required: true,
  },
});
</script>
