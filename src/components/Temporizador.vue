<template>
    <div class="is-flex is-align-items-center is-justify-content-space-between">
        <Cronometro :tempo-em-segundos="tempoEmSegundos" />
        <button class="button" @click="iniciar" :disabled="cronometroRodando">
            <span class="icon">
                <i class="fas fa-play"></i>
            </span>
            <span>play</span>
        </button>
        <button class="button" @click="finalizar" :disabled="!cronometroRodando">
            <span class="icon">
                <i class="fas fa-stop"></i>
            </span>
            <span>stop</span>
        </button>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Cronometro from "./Cronometro.vue";
export default defineComponent({
    // eslint-disable-next-line vue/multi-word-component-names
    name: "Temporizador",
    emits: ['aoTemporizadorFinalizado'],
    data() {
        return {
            tempoEmSegundos: 0,
            cronometro: 0,
            cronometroRodando: false
        };
    },
    methods: {
        iniciar() {
            if (!this.cronometroRodando) {
                this.cronometro = setInterval(() => {
                    this.tempoEmSegundos += 1;
                }, 1000);
                this.cronometroRodando = true
            }
        },
        finalizar() {
            if (this.cronometroRodando) {
                clearInterval(this.cronometro);
                this.cronometroRodando = false
                this.$emit("aoTemporizadorFinalizado", this.tempoEmSegundos)
                this.tempoEmSegundos = 0
            }
        }
    },
    components: { Cronometro }
})
</script>