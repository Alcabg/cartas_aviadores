<script setup>
// Importo la función defineProps de la librería Vue
import { defineProps } from "vue";

// Defino las propiedades esperadas del componente
const props = defineProps(["info"]);

// Concateno la ruta de la imagen con la información de las propiedades de la imagen
const img = "@assets/" + props.info.img;

// Defino las emit que podrá hacer el componente
const emit = defineEmits(["resp"]);

// Función que hace un emit con la información de nombre y victorias del aviador seleccionado
const sendInfo = () => {
  emit("resp", props.info.nombre_aviador, props.info.victorias);
  console.log("emit...");
};
</script>
<template>
  <div class="card-container">
    <div class="card">
      <div class="card-header">
        <!-- Muestro el nombre del aviador -->
        <h2 class="card_title">{{ props.info.nombre_aviador }}</h2>
      </div>
      <div class="card-body">
        <div class="card_info">
          <!-- Muestro la cantidad de victorias del aviador -->
          <p>Victorias: {{ props.info.victorias }}</p>
          <!-- Muestro la nacionalidad del aviador -->
          <p>Nacionalidad: {{ props.info.nacionalidad }}</p>
          <!-- Muestro el avión que pilota el aviador -->
          <p>Avión pilotado: {{ props.info.avion_pilotado }}</p>
        </div>
        <!-- Muestro la imagen del aviador -->
        <img v-bind:src="props.info.img" />
      </div>
      <!-- Botón que emite la información del aviador seleccionado -->
      <button class="card_button" @click="sendInfo">Selecciona</button>
    </div>
  </div>
</template>
<style scoped>
.card-container {
  display: inline-flex;
  align-items: center;
  align-content: center;
  justify-content: center;
}

.card {
  width: 400px;
  border: 1px solid #ddd;
  border-radius: 5px;
  margin: 23px;
  padding: 20px;
  justify-content: center;
  align-items: center;
  gap: 15px;
  box-shadow: 0 0 10px 4px #158b5a;
  background-color: var(--bg-card);
  color: var(--text-card);
}

.card-header {
  border-bottom: 1px solid #ddd;
  padding: 0.75rem;
  text-align: center;
}

.card_title {
  margin: 0;
  font-size: 1.5rem;
}

.card-body {
  display: flex;
  flex-wrap: wrap;
  padding: 1rem;
  justify-content: center;
  align-items: center;
}

.card_info {
  flex: 1;
  margin-right: 1rem;
}

.card_info p {
  margin: 0;
  margin-bottom: 0.5rem;
}

.card_button {
  background-color: rgb(148, 21, 21);
  border: none;
  border-radius: 3px;
  color: #fff;
  cursor: pointer;
  font-size: 1rem;
  padding: 0.5rem 1rem;
  transition: background-color 0.2s ease;
}

.card_button:hover {
  background-color: #158b5a;
}
</style>
