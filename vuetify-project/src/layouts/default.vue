<template>
  <v-app>
    <v-app-bar :elevation="2" rounded>
      <template v-slot:prepend>
        <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      </template>

      <v-app-bar-title>Menu</v-app-bar-title>

      <template v-slot:append>
        <v-btn icon="mdi-heart"></v-btn>
        <v-btn icon="mdi-magnify"></v-btn>
        <v-btn icon="mdi-dots-vertical"></v-btn>
      </template>
    </v-app-bar>

    <v-navigation-drawer v-model="drawer" absolute temporary image="https://scontent.ftij2-1.fna.fbcdn.net/v/t39.30808-6/321664336_1554543251638758_7629285543347536926_n.jpg?stp=cp6_dst-jpg_s960x960&_nc_cat=104&ccb=1-7&_nc_sid=cc71e4&_nc_ohc=rc5xrgLeLc0Q7kNvgGHAhTF&_nc_ht=scontent.ftij2-1.fna&_nc_gid=A3eNPIOQsN3DY77XPjK8FRS&oh=00_AYDRnrGYoY6BuanlHHI6_iZCo9x4D0scKYQGr9V7PFXRyQ&oe=66F25978">
      <v-list>
        <v-list-item v-for="item in items" :key="item.title" :to="item.to">
          <v-icon>{{ item.icon }}</v-icon>
          <v-list-item-title>{{ item.title }}</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-main>
      <router-view />
    </v-main>

    <AppFooter />
  </v-app>
</template>

<script setup>
  import { ref } from 'vue'

  const drawer = ref(false)
  const items = ref([
    { title: 'Inicio', icon: 'mdi-home', to: '/' },
    { title: 'Peliculas', icon: 'mdi-information', to: '/peliculas' },
    { title: 'Pagina 2', icon: 'mdi-email', to: '/pagina2' },
  ])
</script>
