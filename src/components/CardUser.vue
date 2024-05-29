<template>
  <div class="cardUser border border-secondary">
    <div class="d-block">
      <div class="p-2 text-center">
        <img :src="imagenUsuario" :alt="nombreUsuario" class="w-50" />
      </div>
      <div class="p-2 text-center fst-italic fw-bold">
        <span class="w-100">{{ nombreUsuario }}</span>
      </div>
      <form @submit.prevent="enviarMsg">
        <div class="p-2">
          <label class="text-left" for="colorTexto"
            ><small>Color del chat:</small></label
          >
          <input
            id="colorTexto"
            type="color"
            v-model="colorChat"
            class="w-100"
          />
        </div>
        <div class="p-2">
          <label class="text-left" for="textoMensaje"
            ><small>Mensaje:</small></label
          >
          <textarea
            class="textoMensaje w-100"
            rows="3"
            v-model="textoChat"
            @keyup.enter="enviarMsg"
          ></textarea>
          <label class="text-left fst-italic" for="enviarMsg"
            ><small>Click o pulsa ENTER para enviar el mensaje...</small></label
          >
        </div>
        <div class="p-2 text-end">
          <button class="p-1 w-50 btn btn-success">Enviar</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardUser",
  props: {
    imagenUsuario: String,
    nombreUsuario: String,
    alineacion: String,
  },
  data() {
    return {
      colorChat: "#9EE2FF",
      textoChat: "",
    };
  },
  methods: {
    enviarMsg: function () {
      let mensajeChat = {
        autor: this.nombreUsuario,
        color: this.colorChat,
        texto: this.textoChat,
        alineacion: this.alineacion,
      };
      if (this.textoChat.length > 0 && this.textoChat != "\n") {
        this.$emit("enviarMsg", mensajeChat);
      }
      this.textoChat = "";
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.cardUser {
  display: block;
  justify-content: center;
  height: 75vh;
  border-radius: 10px;
}
.cardUser img {
  border-radius: 50%;
}
</style>
