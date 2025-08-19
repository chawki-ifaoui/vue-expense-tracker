<template>
  <v-app-bar
    color="primary"
    class="px-0"
    elevation="0"
  >
    <v-container class="d-flex align-center">
      <v-icon
        icon="mdi-wallet"
        size="24"
        size-md="32"
        class="me-2 me-md-3"
      ></v-icon>
      <v-toolbar-title class="text-h5 text-md-h4 font-weight-bold">
        Expense Tracker
      </v-toolbar-title>
    </v-container>
  </v-app-bar>
</template>

<style scoped>
.v-app-bar {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%) !important;
}
</style>
