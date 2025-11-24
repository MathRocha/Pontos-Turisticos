<script setup>
import { ref } from "vue";
import Cidade from "./components/Cidade.vue";

let cidades = ref([]);
let cidadeSelecionada = ref(null);

fetch("/dados.json")
  .then((resp) => resp.json())
  .then((data) => {
    cidades.value = data;
    selecionarCidade(data[0].id);
  });

const selecionarCidade = (cidadeId) => (cidadeSelecionada.value = cidadeId);
</script>

<template>
  <header>
    <nav>
      <a
        v-for="cidade in cidades"
        class="selecao-ponto-turistico"
        :class="{ selecionada: cidadeSelecionada === cidade.id }"
        @click="selecionarCidade(cidade.id)"
      >
        {{ cidade.nome }}
      </a>
    </nav>
  </header>

  <main>
    <div v-for="cidade in cidades">
      <Cidade v-if="cidadeSelecionada === cidade.id" :cidade="cidade" />
    </div>
  </main>
</template>

<style scoped>
nav {
  margin-bottom: 2em;
}

.selecao-ponto-turistico {
  padding: 1em;
  cursor: pointer;
}

.selecao-ponto-turistico.selecionada {
  background-color: #71baf581;
  transition: all 250ms ease-in;
}
</style>
