<template>
  <div id="app">
    <h2>Ciclos de vida de los componentes</h2>
    <!-- Botones para cambiar entre los componentes -->
    <div class="tags">
      <button
        v-for="(componente, index) in componentes"
        :key="index"
        @click="componenteDinamico = componente.componente"
        :class="{ activo: componenteDinamico === componente.componente }"
        class="tag"
      >
        {{ componente.nombre }}
      </button>
    </div>

    <!-- Muestra el componente que seleccione -->
    <component :is="componenteDinamico" />
  </div>
</template>

<script lang="ts" setup>
import { ref } from "vue";
import Lista from "./components/Lista.vue";
import Tareas from "./components/Tareas.vue";
import DimensionComponente from "./components/DimensionComponente.vue";

// Lista de componentes para elegir
const componentes = [
  { nombre: "Lista", componente: Lista },
  { nombre: "Tareas", componente: Tareas },
  { nombre: "Dimensiones", componente: DimensionComponente },
];

// Componente que se muestra por defecto
const componenteDinamico = ref(componentes[0].componente);
</script>

<style scoped>

h1 {
  font-size: 36px;
  color: #1976d2;
  margin-bottom: 20px;
}
#app {
  font-family: Arial, sans-serif;
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  text-align: center;
}

/* Botones (tags) */
.tags {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

.tag {
  padding: 10px 20px;
  margin: 0 5px;
  font-size: 16px;
  color: #fff;
  background-color: #1976d2;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.3s, transform 0.2s;
}

.tag:hover {
  background-color: #1565c0;
}

.tag.activo {
  background-color: #004ba0;
  font-weight: bold;
  transform: scale(1.1);
}
</style>