<template>
  <footer class="footer flex">
    <section class="contacto centrado-flex">
      <!-- Botón de contacto email -->
      <div class="contacto__mail-linkedin flex">
        <div
          class="socialContainer containerOne"
          tabindex="0"
          @click="mostrarModalCorreo()"
          aria-label="Mostrar dirección de correo"
        >
          <img
            src="/img/ico/mail.svg"
            alt="Icono de correo electrónico"
            class="socialSvg"
          />
        </div>

        <!-- Botón de contacto linkedin -->
        <div class="socialContainer containerTwo" tabindex="0">
          <a
            href="https://www.linkedin.com/in/hugossanchezz/"
            target="_blank"
            aria-label="Ir al perfil de LinkedIn (se abre en nueva ventana)"
          >
            <img
              src="/img/ico/linkedin.svg"
              alt="LinkedIn Icon"
              class="socialSvg"
            />
          </a>
        </div>
      </div>

      <!-- Botón de donaciones "Buy Me a Coffee" -->
      <div class="contacto__donaciones" >
        <img
          src="https://cdn.buymeacoffee.com/buttons/v2/default-white.png"
          alt="Buy Me a Coffee"
          style="height: 50px; width: 200px"
        />
      </div>
    </section>

    <hr />

    <section class="copyright">
      <p>
        © {{ currentYear }} Dia de Cine.
        <a class="autor" href="https://github.com/hugossanchezz" target="_blank"
          >Hugo Sánchez Ciudad</a
        >.
      </p>
    </section>

    <!-- Modales del footer -->
    <div
      v-if="modalCorreoVisible"
      class="overlay centrado-flex"
      @click="cerrarModales"
      tabindex="-1"
    >
      <div
        v-if="modalCorreoVisible"
        class="modal modal-correo flex-column"
        @click="copiarEmail"
        @click.stop
      >
        <h2>Haz <strong>click</strong> para copiar mi email.</h2>

        <hr class="modal__hr" />
        <div class="modal__div flex">
          <div class="email-container flex">
            <!-- Icono del email -->
            <div class="icon-container">
              <img src="/img/ico/mail.svg" alt="Icono de email" />
            </div>
            <!-- Correo electrónico -->

            <p v-if="!esMovil" class="centrado-flex">
              hugosanchezciudad23@gmail.com
            </p>
            <p v-if="esMovil" class="centrado-flex">Copiar mail</p>
          </div>

          <!-- Botón de copiar -->
          <div class="copy-container centrado-flex">
            <img src="/img/ico/copy.svg" alt="Copiar dirección de correo" />
          </div>
        </div>

        <button @click="cerrarModales" class="btn-cerrar centrado-flex">
          <img src="/img/ico/close.svg" alt="Cerrar tarjeta" />
        </button>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: "Footer",
  data() {
    return {
      modalCorreoVisible: false,
      currentYear: new Date().getFullYear(), // Obtener el año actual
    };
  },
  computed: {
    esMovil() {
      return window.innerWidth <= 1024; // Detecta si es móvil/tablet
    },
  },
  methods: {
    mostrarModalCorreo() {
      this.modalCorreoVisible = true;
    },

    cerrarModales() {
      this.modalCorreoVisible = false;
    },
    copiarEmail() {
      // Copiar el correo al portapapeles
      navigator.clipboard
        .writeText("hugosanchezciudad23@gmail.com")
        .then(console.log("Correo copiado al portapapeles."));
    },
  },
};
</script>
