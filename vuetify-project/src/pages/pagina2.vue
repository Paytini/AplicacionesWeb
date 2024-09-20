<template>
  <v-progress-circular class="progress"
    color="blue-lighten-3"
    model-value="20"
    :size="45"
    :width="7"
  ></v-progress-circular>

    <tarjeta class="mt-15"></tarjeta>

    
  </template>
  

  <style scoped>
    .progress {
      position: center;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }
  </style>

