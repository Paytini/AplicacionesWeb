<template>
  <table>
    <thead>
      <tr>
        <th> Indice </th>
        <th>Título</th>
        <th>Calificación</th>
        <th>IMDB</th>
        <th> Acciones </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(pelicula, index) in peliculas" :key="pelicula.id" >
        <td>{{ pelicula.id }}</td>
        <td @click="nombre_pelicula(pelicula)" style="cursor: pointer;">{{ pelicula.movie }}</td>
        <td>{{ pelicula.rating }}</td>
        <td>
          <a :href="pelicula.imdb_url" target="_blank">{{ pelicula.imdb_url }}</a>
        </td>
        <td>
          <v-btn icon="mdi-pencil" @click="$emit('editar_pelicula', pelicula)"></v-btn>
          <v-btn icon="mdi-delete" @click="borrar_informacion(pelicula)" style="cursor: pointer;"></v-btn>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue';

// Definir los props que se recibirán
const props = defineProps({
  peliculas: {
    type: Array,
    required: true,
  },
});

// Emitir eventos
const emit = defineEmits(['nombre_pelicula', 'editar_informacion', 'borrar_informacion','editar_pelicula']);

function nombre_pelicula(pelicula) {
    const payload = {
      movie: pelicula.movie
    };
    emit('nombre_pelicula', payload);
  }

function editar_informacion(pelicula) {
  emit('editar_informacion', pelicula);
}
function borrar_informacion(pelicula) {
  emit('borrar_informacion', pelicula);
}
</script>

<style scoped>
table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  padding: 10px;
  border: 1px solid #ddd;
  text-align: left;
}

th {
  background-color: #12c1e4;
  font-weight: bold;
}

a {
  color: green;
  text-decoration: none;
}
</style>
