<template>
  <main class="columns is-gapeless is-multiline" :class="{ 'modo-escuro': modoEscuroAtivo }">
    <div class="column is-one-quarter">
      <BarraLateral @aoTemaAlterado="trocarTema" />
    </div>
    <div class="column is-three-quarter conteudo">
      <FormularioItem @aoSalvarTarefa="salvarTarefa" />
      <div class="lista">
        <TarefaItem
          v-for="(tarefa, index) in tarefas"
          :key="index"
          :tarefa="tarefa"
        />
       <BoxItem v-if="listaEstaVazia"> Você não está muito produtivo hoje </BoxItem>
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import BarraLateral from "./components/BarraLateral.vue";
import FormularioItem from "./components/Formulario.vue";
import TarefaItem from "./components/Tarefa.vue";
import ITarefa from "./interfaces/ITarefa";
import BoxItem from "./components/Box.vue";

export default defineComponent({
  name: "App",
  components: {
    BarraLateral,
    FormularioItem,
    TarefaItem,
    BoxItem,
  },
  data() {
    return {
      tarefas: [] as ITarefa[],
      modoEscuroAtivo: false
    };
  },
  methods: {
    salvarTarefa(tarefa: ITarefa) {
      this.tarefas.push(tarefa);
    },
    trocarTema(modoEscuroAtivo: boolean) {
      this.modoEscuroAtivo = modoEscuroAtivo
    }
  },
  computed:{
    listaEstaVazia () : boolean{
      return this.tarefas.length === 0
    }
  }
});
</script>

<style scoped>
.lista {
  padding: 1.25rem;
}

main{
  --bg-primario: #fff;
  --texto-primario: #000;
}

main.modo-escuro{
  --bg-primario: #2b2d42;
  --texto-primario: #ddd;
}

.conteudo {
  background-color: var(--bg-primario);
}
</style>
