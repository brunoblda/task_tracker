<template>
  <div class="is-flex is-align-item-center is-justify-content-space-between">
    <CronometroItem :tempoEmSegundos="tempoEmSegundos" />
    <buttonItem
      @clicado="iniciar"
      icone="fas fa-play"
      texto="play"
      :desabilitado="cronometroRodando"
    />
    <buttonItem
      @clicado="finalizar"
      icone="fas fa-stop"
      texto="stop"
      :desabilitado="!cronometroRodando"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import CronometroItem from "./Cronometro.vue";
import ButtonItem from "./ButtonItem.vue";

export default defineComponent({
  name: "TemporizadorItem",
  emits: ["aoTemporizadorFinalizado"],
  components: {
    CronometroItem,
    ButtonItem
  },
  data() {
    return {
      tempoEmSegundos: 0,
      cronometro: 0,
      cronometroRodando: false,
    };
  },
  methods: {
    iniciar() {
      this.cronometroRodando = true;
      this.cronometro = setInterval(() => {
        this.tempoEmSegundos += 1;
      }, 1000);
    },
    finalizar() {
      this.cronometroRodando = false;
      clearInterval(this.cronometro);
      this.$emit("aoTemporizadorFinalizado", this.tempoEmSegundos);
      this.tempoEmSegundos = 0;
    },
  },
});
</script>