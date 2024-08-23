<script setup>
import { ref } from 'vue';

let videojuego = ref({
  nombre: '',
  plataforma: '',
  estado: '',
  puntaje: ''
});
//lista para cargar los videojuegos 
let videojuegos = ref([]);

function cargarvideojuego() {
  // Agregar el videojuego actual a la lista de videojuegos
  videojuegos.value.push({
    nombre: videojuego.value.nombre,
    plataforma: videojuego.value.plataforma,
    estado: videojuego.value.estado,
    puntaje: videojuego.value.puntaje
  });

  // Limpiar el formulario 
  videojuego.value.nombre = '';
  videojuego.value.plataforma = '';
  videojuego.value.estado = '';
  videojuego.value.puntaje = '';
}

</script>

<template>
  <h1>Administración de Videojuegos</h1>
  <h2>Nuevo Videojuego</h2>
  <form @submit.prevent="cargarvideojuego">
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
      </thead>
      <tbody>
        <tr v-for="(vg, index) in videojuegos" :key="index">
          <td><span>{{ vg.nombre }}</span></td>
          <td><span>{{ vg.plataforma }}</span></td>
          <td><span>{{ vg.estado }}</span></td>
          <td><span>{{ vg.puntaje }}</span></td>
          <td><span>+</span></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>
:global(body) {
  background: linear-gradient(to bottom right, green, yellow);
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 20px;
  color: #333;
}

.tabla {
  width: 100%;
  height: auto;
}

thead {
  background-color: #4CAF50;
  color: white;
}

th, td {
  padding: 12px;
  text-align: center;
  border-bottom: 1px solid #ddd;
}

td span {
  display: block;
}

tbody tr:hover {
  background-color: #f1f1f1;
}

tbody tr:nth-child(even) {
  background-color: #f9f9f9;
}

th {
  cursor: pointer;
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
</style>

  