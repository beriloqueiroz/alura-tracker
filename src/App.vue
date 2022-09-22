<template>
  <main class="columns is-gapless is-multiline" :class="modoEscuroAtivo ? 'modo-escuro':''">
    <div class="column is-one-quarter">
      <BarraLateral @alterou-tema="alterarTema" />
    </div>
    <div class="column is-three-quarter conteudo">
      <Formulario @aoSalvarTarefa="salvarTarefa" />
      <div class="lista">
        <Tarefa v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa" />
      </div>
      <Box v-if="listaEstaVazia">
        Você ainda não fez nenhuma tarefa hoje!
      </Box>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import BarraLateral from './components/BarraLateral.vue';
import Formulario from "./components/Formulario.vue";
import Tarefa from './components/Tarefa.vue';
import ITarefa from './interfaces/ITarefa';
import Box from './components/Box.vue';
export default defineComponent({
  name: "App",
  components: { BarraLateral, Formulario, Tarefa, Box },
  data() {
    return {
      tarefas: [] as ITarefa[],
      modoEscuroAtivo: false
    }
  },
  methods: {
    salvarTarefa(tarefa: ITarefa): void {
      this.tarefas.push(tarefa)
    },
    alterarTema(modoEscuroAtivo: boolean): void {
      this.modoEscuroAtivo = modoEscuroAtivo
    }
  },
  computed: {
    listaEstaVazia(): boolean {
      return !this.tarefas.length
    }
  },
});
</script>

<style scoped>
.lista {
  padding: 1.25rem;
}

main {
  --bg-primario: #fff;
  --texto-primario: #000;
}

main.modo-escuro {
  --bg-primario: #2b2d42;
  --texto-primario: #ddd;
}

.conteudo {
  background-color: var(--bg-primario);
  color: var(--texto-primario);
}
</style>
