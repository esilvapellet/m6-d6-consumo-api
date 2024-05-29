<template>
  <div id="app" class="container">
    <h1 class="fw-bold text-uppercase m-3 p-3 text-center">
      Tablero de Mensajes
    </h1>
    <div class="row container" v-if="usuarios.length" id="vistaChat">
      <div class="col-3">
        <CardUser
          :imagenUsuario="usuarios[0].picture.large"
          :nombreUsuario="usuarios[0].name.first"
          alineacion="left"
          @enviarMsg="agregarChat"
          @keypress.enter="agregarChat"
        />
      </div>
      <div class="col-6">
        <CardChat :mensajes="mensajes" />
      </div>
      <div class="col-3">
        <CardUser
          :imagenUsuario="usuarios[1].picture.large"
          :nombreUsuario="usuarios[1].name.first"
          alineacion="right"
          @enviarMsg="agregarChat"
        />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import CardChat from "./components/CardChat.vue";
import CardUser from "./components/CardUser.vue";

export default {
  name: "App",
  components: {
    CardChat,
    CardUser,
  },
  data() {
    return {
      usuarios: [],
      mensajes: [],
    };
  },
  methods: {
    agregarChat: function (nuevoMsg) {
      this.mensajes.push(nuevoMsg);
      console.log(this.mensajes);
    },
  },
  async mounted() {
    try {
      let response = await axios.get("https://randomuser.me/api/?results=2");
      let { data } = response;
      this.usuarios = data.results;
    } catch (error) {
      console.log(error);
      if (error.code == "ERR_NETWORK") {
        return alert(
          "En estos momento el servidor está caído, puede intentar más tarde."
        );
      }
      if (error.response.status == 404) {
        alert("El recurso que está buscando no existe.");
      } else {
        alert("El servidor en estos momentos no puede procesar su solicitud.");
      }
    }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #ffffff;
  width: 90%;
}
body {
  background-image: url("./assets/background.jpg");
  background-size: cover;
  background-repeat: no-repeat;
  color: #ffffff;
}
</style>
