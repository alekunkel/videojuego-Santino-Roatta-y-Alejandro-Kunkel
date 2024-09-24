<script setup>
import { ref, computed } from 'vue';

const videojuego = ref({
  nombre: '',
  plataforma: '',
  estado: '',
  puntaje: ''
});

const videojuegos = ref([]);
const filtroNombre = ref('');
const filtroPlataforma = ref('');
const filtroEstado = ref('');

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
  if (videojuego.value.puntaje && (isNaN(puntajeNumerico) || puntajeNumerico < 1 || puntajeNumerico > 10)) {
    alert('El puntaje debe ser un valor numérico entre 1 y 10.');
    return;
  }
  videojuegos.value.push({
    ...videojuego.value,
    isVisible: false
  });
  videojuego.value = {
    nombre: '',
    plataforma: '',
    estado: '',
    puntaje: ''  
  };
};

const mostrarDetalles = ref(null);

function toggleDetalles(index) {
  mostrarDetalles.value = mostrarDetalles.value === index ? null : index;
}

// Computed property para filtrar videojuegos
const videojuegosFiltrados = computed(() => {
  const lowerFiltroNombre = filtroNombre.value.toLowerCase();
  const lowerFiltroPlataforma = filtroPlataforma.value.toLowerCase();
  const lowerFiltroEstado = filtroEstado.value.toLowerCase();

  return videojuegos.value.filter(vg => 
    vg.nombre.toLowerCase().includes(lowerFiltroNombre) &&
    vg.plataforma.toLowerCase().includes(lowerFiltroPlataforma) &&
    vg.estado.toLowerCase().includes(lowerFiltroEstado)
  );
});
</script>

<template>
  <h1>Administración de Videojuegos</h1>
  <h2>Nuevo Videojuego</h2>
  <form @submit.prevent="cargarvideojuego">
    <label for="nombre">Nombre:</label>
    <input type="text" v-model="videojuego.nombre" placeholder="Ingrese el nombre del videojuego"><br>
    <label for="plataforma">Plataforma:</label>
    <select v-model="videojuego.plataforma">
      <option value="">Seleccione una plataforma</option>
      <option value="xbox">Xbox</option>
      <option value="playstation">PlayStation</option>
      <option value="pc">PC</option>
    </select><br>
    <label for="estado">Estado:</label>
    <select v-model="videojuego.estado">
      <option value="">Seleccione un estado</option>
      <option value="completado">Completado</option>
      <option value="pendiente">Pendiente</option>
      <option value="en proceso">En Proceso</option>
    </select><br>
    <label for="puntaje">Puntaje:</label>
    <input type="text" v-model="videojuego.puntaje" placeholder="Valor numérico del 1 al 10"><br>
    <div class="cargarcss">
      <input type="submit" value="Registrar Videojuego">
    </div>
  </form>
  
  <h2>Filtrar Videojuegos</h2>
  <label for="filtroNombre">Nombre:</label>
  <input type="text" v-model="filtroNombre" placeholder="Filtrar por nombre...">
  
  <label for="filtroPlataforma">Plataforma:</label>
  <select v-model="filtroPlataforma">
    <option value="">Todas las plataformas</option>
    <option value="xbox">Xbox</option>
    <option value="playstation">PlayStation</option>
    <option value="pc">PC</option>
  </select>
  
  <label for="filtroEstado">Estado:</label>
  <select v-model="filtroEstado">
    <option value="">Todos los estados</option>
    <option value="completado">Completado</option>
    <option value="pendiente">Pendiente</option>
    <option value="en proceso">En Proceso</option>
  </select>

  <h2>Videojuegos</h2>
  <div>
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
        <tr v-for="(vg, index) in videojuegosFiltrados" :key="index">
          <td><span>{{ vg.nombre }}</span></td>
          <td><span>{{ vg.plataforma }}</span></td>
          <td><span>{{ vg.estado }}</span></td>
          <td><span>{{ vg.puntaje }}</span></td>
          <td><span><button @click="toggleDetalles(index)">+</button></span></td>
        </tr>
      </tbody>
    </table>
  </div>
  
  <div v-if="mostrarDetalles !== null">
    <h2>Detalles del Videojuego</h2>
    <table>
      <thead>
        <tr>
          <th>Nombre</th>
          <th>Plataforma</th>
          <th>Puntaje</th>
        </tr>
      </thead>
      <tbody>
        <tr v-if="mostrarDetalles !== null">
          <td><span>{{ videojuegos[mostrarDetalles].nombre }}</span></td>
          <td><span>{{ videojuegos[mostrarDetalles].plataforma }}</span></td>
          <td><span>{{ videojuegos[mostrarDetalles].puntaje }}</span></td>
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
  color: chocolate; 
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



