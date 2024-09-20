<template>
  <v-app>
    <v-main>
      <v-toolbar class="custom-toolbar">
        <progreso
          :loading="loading"
          color="blue lighten-3"
        />
      </v-toolbar>

      <v-alert v-if="errorMessage" type="error" class="mt-3">
        {{ errorMessage }}
      </v-alert>
      <router-view v-if="!loading" />
    </v-main>
  </v-app>
</template>

<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import progreso from '../src/components/progressBar.vue';

const loading = ref(false);
const errorMessage = ref('');
const router = useRouter();

function simulateError() {
  // Simulando un error durante la navegación
  if (Math.random() > 0.7) {
    errorMessage.value = 'Ocurrió un error al cargar la página.';
  } else {
    errorMessage.value = '';
  }
}

function delay(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

router.beforeEach(async (to, from, next) => {
  loading.value = true;
  await delay(2000);
  simulateError(); 
  next();
});

router.afterEach(() => {
  loading.value = false;
});
</script>

<style>
.custom-toolbar {
  min-height: 8px;
  height: 8px; 
  padding: 0;
}
.mt-3 {
  margin-top: 16px;
}
</style>
