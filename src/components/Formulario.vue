<template>
    <div class="box formulario">
        <div class="columns">
            <div class="column is-8" role="form" aria-label="Formulário para criação de uma nova task">
                <input type="text" class="input" placeholder="Qual tarefa você deseja iniciar?" v-model="descricao" />
            </div>
            <div class="column">
                <Temporizador @aoTemporizadorFinalizado="finalizarTarefa" />
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Temporizador from './Temporizador.vue';
import ITarefa from '../interfaces/ITarefa'
export default defineComponent({
    // eslint-disable-next-line vue/multi-word-component-names
    name: "Formulário",
    data() {
        return {
            descricao: ''
        }
    },
    emits: ['aoSalvarTarefa'],
    components: { Temporizador },
    methods: {
        finalizarTarefa(tempoDecorrido: number): void {
            const tarefa: ITarefa = {
                duracaoEmSegundos: tempoDecorrido,
                descricao: this.descricao
            }
            this.$emit('aoSalvarTarefa', tarefa)
            this.descricao = ''
        }
    }
})
</script>

<style>
.formulario {
    background-color: var(--bg-primario);
    color: var(--texto-primario);
}
</style>