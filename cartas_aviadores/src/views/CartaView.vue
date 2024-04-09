// Importar las funciones necesarias de Vue
<script setup>
import { ref, onMounted, computed } from "vue";
import PilotsCarta from "../components/PilotsCarta.vue";

// Crear una referencia para el término de búsqueda y para las cartas de pilotos
const search = ref("");
const cards = ref([]);

// Obtener las cartas de pilotos desde un archivo JSON y guardarlas en la referencia "cards"
onMounted(async () => {
  cards.value = await fetch("/src/pilots.json")
    .then((x) => x.json())
    .then((data) => {
      return data.pilots;
    });
});

// Creo una referencia para el mensaje del componente hijo, las cartas seleccionadas y el ganador de la lucha
const msgFromChild = ref("Aún no hay ningún mensaje escrito!");
const selectedCards = ref([]);
const ganador = ref(null);
// const valorGanador = ref(null);

// Función para mostrar el mensaje del componente hijo
const showResp = (nombre_aviador, victorias) => {
  console.log(nombre_aviador, victorias);
  msgFromChild.value = `${nombre_aviador}, ${victorias}`;
};

// Filtrar las cartas de pilotos según el nombre del aviador
const filteredPilots = computed(() => {
  return cards.value.filter((card) => {
    return card.nombre_aviador
      .toLowerCase()
      .includes(search.value.toLowerCase());
  });
});

// Función para seleccionar una carta de piloto
const selectCard = (card) => {
  if (selectedCards.value.length < 2 && !selectedCards.value.includes(card)) {
    selectedCards.value.push(card);
    showResp(card.nombre_aviador, card.victorias);
  }
};

// Función para comprobar si una carta de piloto ha sido seleccionada
const isSelected = (card) => {
  return selectedCards.value.includes(card);
};

// Función para simular una lucha entre dos cartas de piloto y determinar el ganador
const lucha = () => {
  const [card1, card2] = selectedCards.value;
  if (card1.victorias > card2.victorias) {
    ganador.value = card1;
  } else if (card2.victorias > card1.victorias) {
    ganador.value = card2;
  } else {
    ganador.value = null;
  }
};
</script>
// Renderizar la plantilla de la página
<template>
  <h1>Cartas de aviadores</h1>
  <!-- Input para buscar cartas de pilotos -->
  <input v-model="search" type="text" placeholder=" Escribe para buscar..." />

  <!-- Mostrar el mensaje del componente hijo -->
  <p class="mssg__pilots">
    Mensaje del componente PilotsCarta: {{ msgFromChild }}
  </p>

  <!-- Botón para luchar entre dos cartas de piloto -->
  <div v-if="selectedCards.length === 2">
    <button class="luchar" @click="lucha">Luchar!</button>
  </div>
  <!-- Mostrar el ganador de la lucha con un if -->
  <div v-if="ganador">
    <p class="p__win">
      El ganador es {{ ganador.nombre_aviador }} con
      {{ ganador.victorias }} victorias! 🏅🏆
    </p>
  </div>
  <br />
  <!-- Renderizar las cartas de pilotos -->
  <section class="cartes">
    <PilotsCarta
      v-for="card in filteredPilots"
      :key="card.id"
      :info="card"
      @resp="showResp"
      @click="selectCard(card)"
      :class="{ selected: isSelected(card) }"
    />
  </section>
  <div v-if="selectedCards.length === 1">
    <p>
      Carta seleccionada: {{ selectedCards[0].nombre_aviador }} -
      {{ selectedCards[0].victorias }} victorias
    </p>
  </div>
</template>

<style>
h1,
input,
.mssg__pilots,
.p__win {
  margin-left: 1.8rem;
}

.luchar {
  display: flex;
  justify-content: center;
  background-color: #4caf50;
  border: none;
  border-radius: 3px;
  color: #fff;
  cursor: pointer;
  font-size: 1rem;
  padding: 0.5rem 1rem;
  transition: background-color 0.2s ease;
  margin-left: 1.8rem;
}

.cartes {
  margin: 1.8rem;
}
</style>
