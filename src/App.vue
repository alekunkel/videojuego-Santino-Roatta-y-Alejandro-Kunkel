<script setup>
import { ref } from 'vue';

const videojuego = ref({
  nombre: '',
  plataforma: '',
  estado: '',
  puntaje: ''
});

const videojuegos = ref([]);

const cargarvideojuego = () => {
  if (!videojuego.value.nombre || !videojuego.value.plataforma || !videojuego.value.estado) {
    alert('Por favor, complete todos los campos obligatorios (nombre, plataforma, estado).');
    return;
  }
  const puntajeNumerico = Number(videojuego.value.puntaje);
  if (isNaN(puntajeNumerico)) {
  alert('El puntaje debe ser un valor numérico.');
  return;
}
if (videojuego.value.puntaje && (isNaN(puntajeNumerico) || puntajeNumerico < 0 || puntajeNumerico > 10)) {
  alert('El puntaje debe ser un valor numérico entre 1 y 10.');
  return;
}
  videojuegos.value.push({ ...videojuego.value });
  videojuego.value = {
    nombre: '',
    plataforma: '',
    estado: '',
    puntaje: ''  
  };
};

</script>
<template>
  <h1>Administración de Videojuegos</h1>
  <h2>Nuevo Videojuego</h2>
  <form @submit.prevent="cargarvideojuego()">
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
      <div class="cargarcss">
        <input type="submit" value="registrar videojuego">
      </div>
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
          <td><span><button @click="masinfo">+</button></span></td>
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
.cargarcss {
  background-color: red;
  border-radius: 4px;
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
  color:chocolate; 
}

input[type="text"], select {
  margin-bottom: 10px;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
  width: 100%;
}

input[type="submit"]:hover {
  background-color: #45a049;
}
</style>

  
