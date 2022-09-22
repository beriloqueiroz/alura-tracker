<template>
    <header>
        <div class="logo">
            <i>
                <span>B</span>Q
            </i>
            <p>
                tasks
            </p>
        </div>
        <button class="button" @click="alterarTema">
            {{textoBotaoTema}}
        </button>
    </header>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
export default defineComponent({
    name: 'BarraLateral',
    emits: ['alterouTema'],
    data() {
        return {
            modoEscuroAtivo: false
        }
    },
    methods: {
        alterarTema() {
            this.modoEscuroAtivo = !this.modoEscuroAtivo
            this.$emit('alterouTema', this.modoEscuroAtivo)
        }
    },
    computed: {
        textoBotaoTema() {
            return this.modoEscuroAtivo ? 'Desativar modo escuro' : 'Ativar modo escuro'
        }
    }
})
</script>

<style scoped>
header {
    padding: 1rem;
    background: #0d3b66;
    width: 100%;
    height: 100vh;
    text-align: center;
}

header>div>i {
    color: chocolate;
    font-size: 64px;
}

header>div>i>span {
    color: cadetblue;
}

header>div>p {
    color: chocolate;
    font-size: 16px;
    position: absolute;
    bottom: 0;
    right: 70px;
}

.logo {
    position: relative;
    margin-bottom: 24px;
}

@media only screen and (max-width: 768px) {
    header {
        padding: 2.5rem;
        height: auto;
    }
}
</style>