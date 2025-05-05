<template>
    <div class="contenedor-tareas">
      <h2>Lista de Tareas</h2>
      <form @submit.prevent="agregarTarea">
        <input
          v-model="nuevaTarea"
          type="text"
          placeholder="Registrar nueva tarea"
          class="input-tarea"
        />
        <button type="submit" class="btn-agregar">Agregar</button>
      </form>
      <ul class="lista-tareas">
        <li
          v-for="(tarea, index) in tareas"
          :key="index"
          :class="{ existente: index < tareasExistentes }"
          class="item-tarea"
        >
          {{ tarea }}
        </li>
      </ul>
    </div>
  </template>
  
  <script lang="ts" setup>
  import { ref, onBeforeUpdate, onUpdated } from "vue";
  
  // Acá se guarda la lista de tareas
  const tareas = ref<string[]>(["Crear usuario", "Borrar usuario", "Dar permisos"]); // Lista inicial de tareas
  const nuevaTarea = ref<string>(""); // Tarea nueva que vamos a agregar
  let tareasExistentes = tareas.value.length; // Cantidad de tareas que ya estaban antes de modificar
  
  // Hook se ejecuta antes de que la lista cambie
  onBeforeUpdate(() => {
    console.log("Lista aún no modificada"); // Avisamos que todavía no se actualizó
    tareasExistentes = tareas.value.length; // Guardamos cuántas tareas hay antes de modificar
  });
  
  // Hook que se ejecuta después de que la lista cambió
  onUpdated(() => {
    console.log("Lista modificada"); // Avisa que la lista ya se actualizó
  });
  
  // Función para agregar una nueva tarea
  const agregarTarea = () => {
    if (nuevaTarea.value.trim() !== "") {
      tareas.value.push(nuevaTarea.value.trim()); // Agrega la tarea a la lista
      nuevaTarea.value = ""; // Limpia el campo de texto
    }
  };
  </script>
  
  <style scoped>
  /* Contenedor principal */
  .contenedor-tareas {
    font-family: 'Roboto', sans-serif;
    color: #333;
    background-color: #ffffff;
    padding: 20px;
    border-radius: 12px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    max-width: 600px;
    margin: 20px auto;
    border: 1px solid #e0e0e0;
  }
  
  /* Título */
  h2 {
    font-size: 24px;
    text-align: center;
    margin-bottom: 20px;
    color: #1976d2;
  }
  
  /* Formulario */
  form {
    display: flex;
    justify-content: space-between;
    margin-bottom: 20px;
  }
  
  .input-tarea {
    flex: 1;
    padding: 10px;
    font-size: 16px;
    border: 1px solid #ccc;
    border-radius: 8px;
    margin-right: 10px;
  }
  
  .btn-agregar {
    padding: 10px 20px;
    font-size: 16px;
    color: #fff;
    background-color: #1976d2;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  .btn-agregar:hover {
    background-color: #1565c0;
  }
  
  /* Lista de tareas */
  .lista-tareas {
    list-style: none;
    padding: 0;
    margin: 0;
  }
  
  .item-tarea {
    padding: 10px;
    margin-bottom: 10px;
    border: 1px solid #ccc;
    border-radius: 8px;
    background-color: #f9f9f9;
    transition: background-color 0.3s;
  }
  
  /* Estilo para las tareas que ya estaban antes de modificar */
  .item-tarea.existente {
    background-color: #d1e7dd; /* Verde claro */
  }
  </style>