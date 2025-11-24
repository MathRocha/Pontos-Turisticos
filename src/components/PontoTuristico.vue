<script setup>
defineProps(["pontoTuristico"]);
import { ref } from "vue";

let indexFoto = ref(0);
</script>

<template>
  <h2
    class="cabecalho-ponto-turistico"
    :class="{ aberto: pontoTuristico.aberto }"
    @click="pontoTuristico.aberto = !pontoTuristico.aberto"
  >
    {{ pontoTuristico.nome }}
    <span v-if="pontoTuristico.aberto">▲</span>
    <span v-else>▼</span>
  </h2>

  <div v-if="pontoTuristico.aberto" class="corpo-ponto-turistico">
   <p>{{ pontoTuristico.descricao }}</p>

  <div v-if="pontoTuristico.fotos && pontoTuristico.fotos.length > 0" class="galeria-fotos">
    <button @click="indexFoto--" :disabled="indexFoto === 0">◄</button>
    <img :src="pontoTuristico.fotos[indexFoto]" :alt="'Foto de ' + pontoTuristico.nome" width="100%"></img>
    <button @click="indexFoto++" :disabled="indexFoto === pontoTuristico.fotos.length - 1">►</button>
  </div>
</div>
</template>

<style scoped>
.cabecalho-ponto-turistico {
  background-color: #71baf5;
  cursor: pointer;
  padding: 0.5em;
  border-radius: 25px;
  margin-bottom: 0;
}

.cabecalho-ponto-turistico span {
  float: right;
}

.cabecalho-ponto-turistico.aberto {
  border-radius: 25px 25px 0 0;
}

.corpo-ponto-turistico {
  border: 1px solid #71baf5;
  padding: 1em;
}

.galeria-fotos {
  display: flex;
}

.galeria-fotos button {
  background-color: black;
  color: white;
  border: none;
}

.galeria-fotos button:disabled {
  opacity: .25;
}
</style>
