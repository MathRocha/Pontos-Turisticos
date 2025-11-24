<script setup>
defineProps(["cidade"]);
import PontoTuristico from "./PontoTuristico.vue";
</script>

<template>
  <div id="cidade-container">
    <img v-if="cidade.foto" :src="cidade.foto" width="100%"></img>

    <div>
      <h1 id="cidade-titulo">{{ cidade.nome }}</h1>
      <p>{{ cidade.descricao }}</p>
    </div>
  </div>

  <section v-for="pontoTuristico in cidade.pontosTuristicos" class="ponto-turistico">
    <PontoTuristico :pontoTuristico="pontoTuristico" />
  </section>
</template>

<style scoped>
#cidade-container {
  display: grid;
  grid-template-columns: 1fr 2fr;
  gap: 1em;
}

#cidade-titulo {
  margin-top: 0;
}

.ponto-turistico {
  width: 100%;
  margin: 2em 0;
}
</style>
