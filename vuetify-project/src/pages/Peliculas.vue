<template>
  <div>
    <h2 v-if="seleccionado.movie"> Película Seleccionada: {{ seleccionado.movie }}</h2>

    <div v-if="mostrarFormulario" class="modal">
      <PeliculaEdit 
        :pelicula="seleccionado" 
        @editar_informacion="guardarCambios" 
      />
    </div>
    
    <PeliculasTable 
      :peliculas="peliculas" 
      @nombre_pelicula="funcion_nombre"
      @editar_pelicula="mostrarFormularioEdicion"
      @borrar_informacion="borrar_pelicula"
    />
    
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import PeliculasTable from '../components/Tabla_peliculas.vue';
import PeliculaEdit from '../components/cuadro_editar.vue';

const peliculas = ref([]);
const seleccionado = ref({});
const mostrarFormulario = ref(false);

function funcion_nombre(payload) {
  seleccionado.value = payload;
}

function mostrarFormularioEdicion(pelicula) {
  seleccionado.value = pelicula;
  mostrarFormulario.value = true;
}

function guardarCambios(peliculaEditada) {
  console.log("Película editada guardada:", peliculaEditada);
  const index = peliculas.value.findIndex(p => p.id === peliculaEditada.id);
  if (index !== -1) {
    peliculas.value[index] = { ...peliculaEditada };
    console.log("Película actualizada en la lista:", peliculas.value[index]);
  } else {
    console.error("No se encontró la película para actualizar.");
  }
  mostrarFormulario.value = false;
}



function borrar_pelicula(pelicula) {
  const confirmacion = confirm(`¿Estás seguro de que deseas borrar la película "${pelicula.movie}"?`);
  if (confirmacion) {
    console.log("Película a borrar:", pelicula.movie);
    peliculas.value = peliculas.value.filter(p => p.movie !== pelicula.movie);
  } else {
    console.log("Borrado cancelado.");
  }
}

onMounted(async () => {
  try {
    const response = await fetch('https://dummyapi.online/api/movies');
    const data = await response.json();
    peliculas.value = data;
  } catch (error) {
    console.error('Error fetching peliculas:', error);
  }
});
</script>

<style scoped>  
  .modal {
    display: flex;
    justify-content: center;
    align-items: center;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5); /* Fondo semi-transparente */
    z-index: 1000; /* Asegúrate de que esté por encima de otros elementos */
  }


</style>
