<script setup>
import { ref } from 'vue';

const videojuego = ref({
  nombre: '',
  plataforma: '',
  puntaje: '',
  estado: '',
});
const emviar = () => {
  console.log('Videojuego cargado:', videojuego.value);
  videojuego.value = {
    nombre: '',
    plataforma: '',
    puntaje: '',
    estado: '',
  };
};
</script>
<template>
  <h1>Administracion de Videojuegos</h1>
  <h2>Nuevo videojuego</h2>
  <form @submit.prevent="cargardocente">
    <div>
      <label for="nombre">Introduce el nombre del videojuego:</label>
      <input type="text" v-model="videojuego.nombre" id="nombre">
    </div>

    <div>
      <h2>Plataforma</h2>
      <select v-model="videojuego.plataforma">
        <option value="">Seleccione una plataforma</option>
        <option value="xbox">Xbox</option>
        <option value="playstation">PlayStation</option>
        <option value="pc">PC</option>
      </select>
    </div>

    <div>
      <h2>Puntaje</h2>
      <label for="puntaje">Introduce el puntaje del videojuego:</label>
      <input type="text" v-model="videojuego.puntaje" id="puntaje">
    </div>

    <div>
      <h2>Estado del Videojuego</h2>
      <select v-model="videojuego.estado">
        <option value="">Seleccione un estado</option>
        <option value="completado">Completado</option>
        <option value="pendiente">Pendiente</option>
        <option value="en proceso">En Proceso</option>
      </select>
    </div>

    <div>
      <input type="submit" value="Enviar">
    </div>
  </form>
  <table>
    <thead>
      <tr>
        <th>Nombre</th>
        <th>Plataforma</th>
        <th>Estado</th>
        <th>Puntaje</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>{{ videojuego.nombre }}</td>
        <td>{{ videojuego.plataforma }}</td>
        <td>{{ videojuego.estado }}</td>
        <td>{{ videojuego.puntaje }}</td>
      </tr>
    </tbody>
  </table>
</template>
<style scoped>
</style>
