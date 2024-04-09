<!-- Import de los componentes -->
<script setup>
import { RouterLink, RouterView } from "vue-router";
import Hello from "./components/Hello.vue";
import { ref } from "vue";

// Declaramos una variable reactiva para el tema dark
const theme = ref("dark");
</script>
<!-- Estructura del componente -->
<template>
  <main class="themed" v-bind:class="theme">
    <header>
      <div class="wrapper">
        <!-- Renderizado del componente HelloWorld -->
        <Hello msg="Batalla de aviadores de la Primera Guerra Mundial!" />
        <!-- <nav>
           Links de navegación usando RouterLink de vue-router 
          <RouterLink to="/">Home</RouterLink>
          <RouterLink to="/about">About</RouterLink>
          <RouterLink to="/cartas">Cartas</RouterLink>
        </nav> -->
      </div>

      <!-- Inserto la imagen del avión Fokker -->
      <img
        alt="Vue logo"
        class="logo"
        src="@/assets/fokker.png"
        width="500"
        height="500"
      />
    </header>
    <!-- Creo un div con dos radiobuttons para cambiar el tema -->
    <div class="settings">
      Theme:
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="24"
        height="24"
        viewBox="0 0 24 24"
        fill="none"
        stroke="currentColor"
        stroke-width="2"
        stroke-linecap="round"
        stroke-linejoin="round"
        class="icon icon-tabler icons-tabler-outline icon-tabler-arrow-right"
      >
        <path stroke="none" d="M0 0h24v24H0z" fill="none" />
        <path d="M5 12l14 0" />
        <path d="M13 18l6 -6" />
        <path d="M13 6l6 6" />
      </svg>
      {{ theme }}
      <label id="dark" for="dark"
        ><svg
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill=" rgb(244,243,224)"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
          class="icon icon-tabler icons-tabler-outline icon-tabler-moon"
        >
          <path stroke="none" d="M0 0h24v24H0z" fill="none" />
          <path
            d="M12 3c.132 0 .263 0 .393 0a7.5 7.5 0 0 0 7.92 12.446a9 9 0 1 1 -8.313 -12.454z"
          /></svg
      ></label>
      <input
        type="radio"
        name="theme"
        id="dark"
        value="dark"
        v-model="theme"
        checked
      />
      <label id="light" for="light"
        ><svg
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill=" rgb(244,128,55)"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
          class="icon icon-tabler icons-tabler-outline icon-tabler-sun"
        >
          <path stroke="none" d="M0 0h24v24H0z" fill="none" />
          <path d="M12 12m-4 0a4 4 0 1 0 8 0a4 4 0 1 0 -8 0" />
          <path
            d="M3 12h1m8 -9v1m8 8h1m-9 8v1m-6.4 -15.4l.7 .7m12.1 -.7l-.7 .7m0 11.4l.7 .7m-12.1 -.7l-.7 .7"
          /></svg
      ></label>
      <input
        type="radio"
        name="theme"
        id="light"
        value="light"
        v-model="theme"
      />
      <br />
    </div>
    <!-- Componente RouterView para mostrar las vistas -->
    <RouterView />
  </main>
</template>

<style scoped>
:root {
  --bg-color: #181818;
  --text-color: hsla(160, 100%, 37%, 1);
  --bg-card: hsla(160, 100%, 37%, 1);
  --text-card: #222;
}

.themed.dark {
  --bg-color: #181818;
  --text-color: hsla(160, 100%, 37%, 1);
  --bg-card: #1c3320;
  --text-card: rgb(187, 187, 187);
}

.themed.light {
  --text-color: #111;
  --bg-color: #e2e2e2;
  --bg-card: rgb(179, 179, 179);
  --text-card: #181818;
}

.themed {
  background-color: var(--bg-color);
  color: var(--text-color);
}

.settings {
  display: flex;
  font-weight: bold;
  align-items: center;
  margin-left: 1.8rem;
}

#dark,
#light {
  margin-left: 10px;
}
input[type="radio"] {
  accent-color: rgb(148, 21, 21);
}
/* .settings label {
  margin: 0.5rem;
} */

header {
  line-height: 1.5;
  max-height: fit-content;
  max-width: fit-content;
}

.logo {
  display: block;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
