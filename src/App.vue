<script setup>
import { ref } from 'vue';

const videojuego = ref({
  nombre: '',
  plataforma: '',
  estado: '',
  puntaje: ''
});

const videojuegos = ref([]);

function cargarVideojuego() {
  // Validar que todos los campos requeridos estén completos
  if (!videojuego.value.nombre || !videojuego.value.plataforma || !videojuego.value.estado) {
    alert('Por favor, complete todos los campos requeridos (nombre, plataforma, estado).');
    return;
  }

  // Validar que el puntaje sea numérico si está completado
  if (videojuego.value.puntaje && isNaN(videojuego.value.puntaje)) {
    alert('El puntaje debe ser un valor numérico.');
    return;
  }

  // Validar que el puntaje esté entre 1 y 10 si está completado
  if (videojuego.value.puntaje && (videojuego.value.puntaje < 1 || videojuego.value.puntaje > 10)) {
    alert('El puntaje debe estar entre 1 y 10.');
    return;
  }

  // Agregar el videojuego a la lista
  videojuegos.value.push({ ...videojuego.value });

  // Limpiar el formulario
  videojuego.value = {
    nombre: '',
    plataforma: '',
    estado: '',
    puntaje: ''
  };
} 
</script>
<template>
  <h1>Administración de Videojuegos</h1>
  <h2>Nuevo Videojuego</h2>
  <form @submit.prevent="cargarVideojuego">
      <label for="nombre">nombre:</label>
      <input type="text" v-model="videojuego.nombre" placeholder="ingrese aqui el videojuego"><br>
      <label for="">Plataforma</label>
      <select v-model="videojuego.plataforma">
        <option value="">PC | Playstation | Xbox</option>
        <option value="xbox">Xbox</option>
        <option value="playstation">PlayStation</option>
        <option value="pc">PC</option>
      </select><br>
      <label for="">estado</label>
      <select v-model="videojuego.estado">
        <option value="">Pendiente | Jugando | Completado </option>
        <option value="completado"> Completado </option>
        <option value="pendiente">Pendiente </option> 
        <option value="en proceso">En Proceso </option>
      </select><br>
      <label for="puntaje">Puntaje:</label>
      <input type="text" v-model="videojuego.puntaje" placeholder="valor numerico del 1 al 10"><br>
      <input type="submit" value="registrar videojuego">
    
  </form>

  <h2> Videojuegos</h2>
  <div>
    <label for="">Nombre</label>
    <input type="text">
    <label for="">Plataforma</label>
      <select v-model="videojuego.plataforma">
        
        <option value="xbox">Xbox</option>
        <option value="playstation">PlayStation</option>
        <option value="pc">PC</option>
      </select>
      <label for="">estado</label>
      <select v-model="videojuego.estado">
        
        <option value="completado"> Completado </option>
        <option value="pendiente">Pendiente </option> 
        <option value="en proceso">En Proceso </option>
      </select>
  </div>
  <div class="tabla">
    <table>
      <thead>
        <tr>
          <th>Nombre</th>
          <th>Plataforma</th>
          <th>Estado</th>
          <th>Puntaje</th>
          <th>Más info</th>
        </tr>
        <tbody>
  <tr v-for="(vg, index) in videojuegos" :key="index">
    <td><span>{{ vg.nombre }}</span></td>
    <td><span>{{ vg.plataforma }}</span></td>
    <td><span>{{ vg.estado }}</span></td>
    <td><span>{{ vg.puntaje }}</span></td>
    <td><span>+</span></td>
  </tr>
</tbody>
      </thead>
    </table>
  </div>
   </template>
<style scoped>
:global(body) {
  background: linear-gradient(to bottom right, green, yellow);
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 20px;
  color:chocolate; 
}

input[type="text"], select {
  margin-bottom: 10px;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
  width: 100%;
}

input[type="submit"] {
  background-color: #4CAF50;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

input[type="submit"]:hover {
  background-color: #45a049;
}

.tabla {
  margin-top: 20px;
  overflow-x: auto;
}

table {
  width: 100%;
  border-collapse: collapse;
  background-color: #f9f9f9;
}

table th,
table td {
  padding: 12px 15px;
  border: 1px solid #ddd;
  text-align: left;
}

table th {
  background-color: #4CAF50;
  color: white;
}

table tr:nth-child(even) {
  background-color: #f2f2f2;
}

table tr:hover {
  background-color: #e9e9e9;
}

table td span {
  display: inline-block;
  padding: 8px;
  border-radius: 4px;
}

table td span:hover {
  background-color: #d9d9d9;
  cursor: pointer;
}

table th:last-child,
table td:last-child {
  text-align: center;
}

table td:last-child span {
  font-weight: bold;
  color: #4CAF50;
  font-size: 1.2em;
}
</style>

