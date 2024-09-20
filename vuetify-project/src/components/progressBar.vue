<template>
    <v-progress-linear
      v-if="loading"
      indeterminate
      color="blue lighten-3"
      height="8"
      absolute
      top
      style="z-index: 9999; width: 100%;"
    ></v-progress-linear>
  </template>
  
  <script setup>
  import { defineProps } from 'vue';
  
  const props = defineProps({
    loading: {
      type: Boolean,
      required: true
    },
    color: {
      type: String,
      default: 'primary'
    }
  });
  </script>
  
  <style scoped>
  </style>
  