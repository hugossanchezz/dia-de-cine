<template>
  <div class="body-grid-index">
    <!-- Header común -->
    <Header />
    
    <!-- Carrusel -->
    <section class="carrusel flex">
      <div id="carrusel__items" class="carrusel__items flex">
        <!-- Espacio para el carrusel que se cargará dinámicamente con JavaScript -->
      </div>
    </section>

    <!-- Contenido principal -->
    <section class="main-grid centrado-flex">
      <!-- Animación de carga -->
      <div id="loader" class="loader" v-if="loading"></div>

      <!-- Contenido principal -->
      <div
        id="contenido-mostrar"
        class="contenido-mostrar margin-contenedor-noticias flex-column"
        v-show="!loading"
      >
        <div class="titulo-noticias centrado-flex">
          <h1>
            Sección de Noticias 
            <span class="fecha">{{ fechaNoticias }}</span>
          </h1>
        </div>
        <hr />

        <div id="noticias-container" class="noticias-container">
          <!-- Espacio de las noticias con el Api NewsAPI -->
        </div>

        <div class="noticias-boton-container centrado-flex">
          <button
            id="recargar-noticias"
            class="button-submit button-submit-pequenio"
            @click="mostrarMasNoticias"
          >
            Mostrar más noticias
          </button>
        </div>
      </div>
    </section>

    <!-- Estrenos -->
    <aside>
      <div class="titulo-estrenos centrado-flex">
        <h1>
          Próximos estrenos 
          <span class="fecha">{{ fechaEstrenos }}</span>
        </h1>
      </div>
      <hr />
      <section id="estrenos-container" class="estrenos-container grid">
        <!-- Espacio de los estrenos de 2025 -->
      </section>
    </aside>

    <!-- Footer común -->
    <Footer />
  </div>
</template>

<script>
import { mostrarCarrusel } from "/src/js/carrusel.js";
import { mostrarEstrenos } from "/src/js/estrenos.js";
import { mostrarNoticias } from "/src/js/noticias.js";

import Header from "/src/components/Header.vue";
import Footer from "/src/components/Footer.vue";

export default {
  name: "IndexView",
  components: {
    Header,
    Footer,
  },
  data() {
    return {
      loading: true,
      fechaNoticias: "",
      fechaEstrenos: "",
      numNoticas: 8,
      numEstrenos: 15,
    };
  },
  async mounted() {
    this.fechaNoticias = new Date().toLocaleDateString();
    this.fechaEstrenos = new Date().getFullYear();

    mostrarCarrusel();
    mostrarEstrenos(this.numEstrenos);
    await mostrarNoticias(this.numNoticas);

    this.mostrarContenido();
  },
  methods: {
    mostrarContenido() {
      setTimeout(() => {
        this.loading = false;
      }, 100);
    },
    async mostrarMasNoticias() {
      this.numNoticas += 8;
      await mostrarNoticias(this.numNoticas);
    },
  },
};
</script>
