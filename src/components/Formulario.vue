<template>
  <div class="box formulario">
    <div class="column">
      <div
        class="column is-8"
        role="form"
        aria-label="Formulario para criação de uma nova tarefa"
      >
        <input
          type="text"
          class="input"
          placeholder="Qual tarefa voce deseja iniciar"
          v-model="descricao"
        />
        <div class="column">
          <Temporizador @aoTemporizadorFinalizado="finalizarTarefa" />
        </div>
      </div>
    </div>
  </div>
</template>

<script lang='ts'>
import ITarefa from "@/interfaces/ITarefa";
import { defineComponent } from "vue";
import Temporizador from "./Temporizador.vue";
export default defineComponent({
  // eslint-disable-next-line
  name: "Formulario",
  components: {
    Temporizador,
  },
  methods: {
    finalizarTarefa(tempoDecorrido: number): void {
      const tarefa = {
        duracaoEmSegundos: tempoDecorrido,
        descricao: this.descricao,
      } as ITarefa;
      this.$emit("aoSalvarTarefa", tarefa);
      this.descricao = "";
    },
  },
  data() {
    return {
      descricao: "",
    };
  },
  emits: ["aoSalvarTarefa"],
});
</script>
<style >
.formulario {
  color: var(--texto-primario);
  background-color: var(--bg-primario);
}
</style>
