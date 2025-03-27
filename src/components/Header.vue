<template>
  <!-- Encabezado -->
  <header class="flex">
    <section class="section-logo flex">
      <router-link to="/">
        <img id="logo" :src="iconoLogo" alt="Logo" />
      </router-link>
    </section>

    <nav class="header__nav centrado-flex">
      <section
        class="container-nav-items flex"
        :class="{ 'menu-abierto': menuAbierto }"
      >
        <div class="nav__item">
          <router-link to="/peliculas" class="centrado-flex font-size-pequenio">
            Películas
          </router-link>
        </div>
        <div class="nav__item">
          <router-link to="/series" class="centrado-flex font-size-pequenio">
            Series
          </router-link>
        </div>
        <div class="nav__item">
          <router-link to="/comunidad" class="centrado-flex font-size-pequenio">
            Comunidad
          </router-link>
        </div>
        <div class="nav__item">
          <router-link to="/nosotros" class="centrado-flex font-size-pequenio">
            Nosotros
          </router-link>
        </div>
        <div class="nav__item">
          <router-link
            to="/mi-espacio"
            class="centrado-flex font-size-pequenio"
          >
            Mi espacio
            <img
              class="item__bookmark"
              src="/img/ico/bookmark.svg"
              alt="Icono de guardado"
            />
          </router-link>
        </div>
      </section>
    </nav>

    <section id="acciones" class="acciones flex">
      <div v-if="esMovil" class="menu-hamburguesa flex" @click="toggleMenu">
        <img class="menu-icono" :src="iconoMenu" alt="Icono de menú" />
      </div>

      <input
        v-if="buscar"
        id="input-busqueda"
        class="oculto input-busqueda inputForm input"
        type="text"
        placeholder="Buscar..."
      />

      <div class="acciones__container centrado-flex">

        <div v-if="!buscar" class="container__login">
          <div v-show="!registrado" class="boton-registrarse">
            <router-link to="/perfil/registro" class="centrado-flex">
              Registrarse
            </router-link>
          </div>
          <router-link v-show="registrado" to="/perfil">
            <img
              class="login__icono"
              src="/img/ico/user-naranja.svg"
              alt="Icono de inicio de sesión"
            />
          </router-link>
        </div>

        <div class="oculto container__busqueda">
          <img
            class="busqueda__icono"
            :src="iconoLupa"
            alt="Icono de búsqueda"
            @click="buscar = !buscar"
          />
        </div>
      </div>
    </section>
  </header>
</template>

<script>

export default {
  name: "Header",
  data() {
    return {
      menuAbierto: false,
      esMovil: window.innerWidth <= 1024,
      buscar: false,
      registrado: false,
    };
  },
  mounted() {
    window.addEventListener("resize", this.actualizarTamano);
  },
  beforeUnmount() {
    window.removeEventListener("resize", this.actualizarTamano);
  },
  computed: {
    iconoLogo() {
      return this.esMovil
        ? "/img/logo-no-cd.png"
        : "/img/logo-no-subtitulo.png";
    },
    iconoMenu() {
      return this.menuAbierto
        ? "/img/ico/close.svg"
        : "/img/ico/menu-hamburguesa.svg";
    },
    iconoLupa() {
      return this.buscar ? "/img/ico/close.svg" : "/img/ico/lupa.svg";
    },
  },
  methods: {
    toggleMenu() {
      this.menuAbierto = !this.menuAbierto;
    },
    actualizarTamano() {
      this.esMovil = window.innerWidth <= 1024;
      if (!this.esMovil) {
        this.menuAbierto = false;
      }
    },
  },
};
</script>
