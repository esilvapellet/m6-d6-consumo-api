<template>
  <div class="cardChat border border-secondary">
    <div
      id="scrollableDiv"
      class="msg d-flex flex-column"
      v-for="(mensaje, index) in mensajes"
      :key="index"
      :style="{
        textAlign: mensaje.alineacion,
      }"
    >
      <div>
        <span class="fs-6"
          ><small>{{ mensaje.autor }}</small></span
        >
        <div>
          <span
            :style="{
              backgroundColor: mensaje.color,
              textAlign: mensaje.alineacion,
            }"
            class="fs-5 rounded inline-block"
            id="cajaTexto"
          >
            {{ mensaje.texto }}
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardChat",
  props: {
    mensajes: Array,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.cardChat {
  background-image: url("../assets/background-2.jpg");
  background-size: contain;
  background-repeat: repeat;
  background-position: center center;
  background-color: bisque;
  height: 75vh;
  overflow-y: scroll;
  display: flex;
  flex-direction: column;
}
.msg {
  padding: 5px;
  color: #000000;
}
#cajaTexto {
  padding: 2px 12px;
}
</style>
