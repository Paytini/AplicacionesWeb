<template>
    <div class="text-center">
      <v-menu transition="fab-transition">
        <template v-slot:activator="{ props }">
          <v-btn
            color="primary"
            dark
            v-bind="props"
          >
            Transicion Tarjeta
          </v-btn>
        </template>
        <v-list>
            <RouterLink to="/pagina2">Pagina 2</RouterLink>
            <v-divider></v-divider>
            <RouterLink to="/peliculas">Peliculas IMBD</RouterLink>
        </v-list>
      </v-menu>
    </div>
  </template>