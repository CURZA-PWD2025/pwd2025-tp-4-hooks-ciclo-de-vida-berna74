<template>
  <div class="contenedor-dimensiones">
    <h2>Dimensiones del Componente</h2>
    <p>Ancho: {{ ancho }}px</p>
    <p>Alto: {{ alto }}px</p>
  </div>
</template>

<script lang="ts" setup>
import { ref, onMounted, onUnmounted } from "vue";

// Variables reactivas para almacenar las dimensiones
const ancho = ref(window.innerWidth);
const alto = ref(window.innerHeight);

// Función para actualizar las dimensiones
const actualizarDimensiones = () => {
  ancho.value = window.innerWidth;
  alto.value = window.innerHeight;
};

// Hook que se ejecuta cuando el componente se monta
onMounted(() => {
  console.log("Componente montado, escuchando eventos de resize");
  window.addEventListener("resize", actualizarDimensiones); // Escuchar el evento resize
});

// Hook que se ejecuta cuando el componente se desmonta
onUnmounted(() => {
  console.log("Componente desmontado, removiendo eventos de resize");
  window.removeEventListener("resize", actualizarDimensiones); // Remover el evento resize
});
</script>

<style scoped>

.contenedor-dimensiones {
  font-family: 'Roboto', sans-serif;
  color: #333;
  background-color: #f9f9f9;
  padding: 20px;
  border-radius: 12px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  max-width: 400px;
  margin: 20px auto;
  border: 1px solid #e0e0e0;
  text-align: center;
}


h2 {
  font-size: 24px;
  color: #1976d2;
  margin-bottom: 10px;
}


p {
  font-size: 18px;
  color: #555;
  margin: 5px 0;
}
</style>