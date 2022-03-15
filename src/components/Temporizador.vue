<template>
  <div class="is-flex is-align-items-center is-justify-content-space-between">
    <Cronometro :tempoEmSegundos="tempoEmSegundos" />
    <Button
      texto="Play"
      icone="fas fa-play"
      :disabled="cronometroRodando"
      @clicked="iniciar"
    />
    <Button
      texto="Stop"
      icone="fas fa-stop"
      :disabled="!cronometroRodando"
      @clicked="finalizar"
    />
  </div>
</template>



<script>
import { defineComponent } from "vue";
import Cronometro from "./Cronometro.vue";
import Button from "./Button.vue";
export default defineComponent({
  // eslint-disable-next-line
  name: "Temporizador",
  emits: ["aoTemporizadorFinalizado"],
  components: {
    Cronometro,
    Button,
  },
  methods: {
    iniciar() {
      this.cronometro = setInterval(() => {
        this.tempoEmSegundos++;
      }, 1000);
      this.cronometroRodando = true;
    },
    finalizar() {
      clearInterval(this.cronometro);
      this.cronometroRodando = false;
      this.$emit("aoTemporizadorFinalizado", this.tempoEmSegundos);
      this.tempoEmSegundos = 0;
    },
  },
  data() {
    return {
      tempoEmSegundos: 0,
      cronometro: 0,
      cronometroRodando: false,
    };
  },
});
</script>
