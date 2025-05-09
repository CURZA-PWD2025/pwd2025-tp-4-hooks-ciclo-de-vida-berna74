<template>
  <h2>Profesiones</h2>
  <div class="contenedor-lista">
    <div v-if="cargando" class="cargando">
      <span class="indicador-carga"></span> Cargando profesiones...
    </div>
    <ul v-else class="lista-profesiones">
      <li v-for="profesion in profesiones" :key="profesion.id" class="item-profesion">
        <div class="encabezado-profesion">
          <strong class="nombre-profesion">{{ profesion.nombre }}</strong>
        </div>
        <p class="descripcion-profesion">{{ profesion.descripcion }}</p>
      </li>
    </ul>
  </div>
</template>

<script lang="ts" setup>
import { ref, onMounted } from "vue";
import profesionesData from "../../../resource/profesiones";

// Guardar la lista de profesiones
const profesiones = ref([]); // Lista vacía al principio
const cargando = ref(true); // Estado para saber si estamos cargando

// Cuando el componente se monta, simula una carga de datos
onMounted(() => {
  console.log("Cargando profesiones...");
  setTimeout(() => {
    profesiones.value = profesionesData; // Carga las profesiones
    cargando.value = false; // Termina de cargar
    console.log("Profesiones cargadas");
  }, 3000); // Simula una demora de 3 segundos
});
</script>

<style scoped>

.contenedor-lista {
  font-family: 'Roboto', sans-serif;
  color: #333333; /* Texto oscuro */
  background-color: #ffffff; /* Fondo blanco */
  padding: 30px;
  border-radius: 15px;
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.1);
  max-width: 800px;
  margin: 40px auto;
  border: 1px solid #e0e0e0; /* Gris claro */
}


h2 {
  font-size: 28px;
  text-align: center;
  margin-bottom: 30px;
  color: #1976d2; /* Azul cielo */
  font-weight: bold;
  border-bottom: 2px solid #1976d2;
  padding-bottom: 10px;
}

/* Lista de profesiones */
.lista-profesiones {
  list-style: none;
  padding: 0;
  margin: 0;
}

.item-profesion {
  background: linear-gradient(135deg, #e3f2fd, #bbdefb); /* Azul claro */
  border: 1px solid #90caf9; /* Azul suave */
  border-radius: 12px;
  padding: 20px;
  margin-bottom: 20px;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.item-profesion:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 20px rgba(25, 118, 210, 0.3); /* Sombra azul */
}

/* Encabezado de cada profesión */
.encabezado-profesion {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 10px;
}

.nombre-profesion {
  font-size: 20px;
  color: #1976d2; /* Azul cielo */
  font-weight: bold;
}

/* Descripción de cada profesión */
.descripcion-profesion {
  font-size: 16px;
  color: #555555; /* Gris oscuro */
  line-height: 1.8;
}

/* Carga */
.cargando {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 18px;
  color: #1976d2; 
}

.indicador-carga {
  width: 30px;
  height: 30px;
  border: 4px solid #e0e0e0; 
  border-top: 4px solid #1976d2; 
  border-radius: 50%;
  animation: girar 1s linear infinite;
  margin-right: 12px;
}

@keyframes girar {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>