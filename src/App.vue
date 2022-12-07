<template>
  <v-app>
    <v-main>
      <Cabecalho />
      <v-container fluid class="mt-5">
        <v-row justify="center" align="center">
          <v-col class="text-center items-center">
            <Home />
          </v-col>
        </v-row>
      </v-container>
    </v-main>
    <v-footer class="text-center pa-8" style="background: #d71c23">
      <v-row justify="center" align="center">
        <v-col class="text-center items-center">
          <h3 class="white--text">
            Diego Chaves - Guilherme de Sá - Alessandra Oliveira - Lucas
            Ferreira
          </h3>
        </v-col>
      </v-row>
    </v-footer>
  </v-app>
</template>

<script>
import Cabecalho from "./components/Cabecalho";
import Home from "./components/Home";

export default {
  name: "App",

  components: {
    Cabecalho,
    Home,
  },

  data: () => ({
    //
  }),
};
</script>
