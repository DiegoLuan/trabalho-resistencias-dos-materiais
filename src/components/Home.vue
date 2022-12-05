<template>
  <div id="home">
    <v-row>
      <v-col>
        <h1 class="mb-3">Calculadora para Resistências dos materiais</h1>
        <p>
          A aplicação foi feita com intuito de realizar cálculos específicos
          para fixação e sustentação de parafusos no teto.
        </p>
      </v-col>
    </v-row>
    <v-row justify="center" align="center">
      <v-col cols="6" style="max-width: 600px">
        <v-card class="text-center">
          <v-card-title class="mb-3"
            >Equação para diâmetro do parafuso</v-card-title
          >
          <v-card-subtitle>d = √4/π x (P/σ_adm)</v-card-subtitle>
          <v-btn @click="dialog_diametro = true" color="success" class="ma-3"
            >Calcular</v-btn
          >
        </v-card>
      </v-col>
      <v-col cols="6" style="max-width: 600px">
        <v-card class="text-center">
          <v-card-title class="mb-3"
            >Equação para espessura do teto</v-card-title
          >
          <v-card-subtitle
            >h = 1/(π x d_arruela) x (P/τ_cisalhamento)</v-card-subtitle
          >
          <v-btn @click="dialog_espessura = true" color="success" class="ma-3"
            >Calcular</v-btn
          >
        </v-card>
      </v-col>
    </v-row>

    <v-row>
      <v-col>
        <div class="text-center">
          <!-- Modal diametro-->
          <v-dialog v-model="dialog_diametro" width="500">
            <v-card>
              <v-card-title
                class="text-center"
                style="background: #d71c23; color: white"
              >
                Equação para equação do parafuso</v-card-title
              >
              <v-card-text class="pa-5" style="color: #000">
                <h3 class="mb-5">d = √4/π x (P/σ_adm)</h3>
                <v-text-field
                  v-model="forca_diametro"
                  suffix="N"
                  label="Força"
                ></v-text-field>
                <v-text-field
                  v-model="tensao_adm"
                  suffix="Pa"
                  label="Tensão Admissível"
                ></v-text-field>
                <v-text-field
                  readonly
                  v-model="diametro_parafuso"
                  suffix="mm"
                  label="Resposta - Diâmetro Parafuso"
                ></v-text-field>

                <div class="mb-7">
                  <v-btn
                    @click="limpar_diametro"
                    color="red"
                    class="mr-3 white--text"
                    >Limpar Campos</v-btn
                  >
                  <v-btn @click="calcular_diametro" color="primary"
                    >Calcular</v-btn
                  >
                </div>

                <v-card-text>
                  <h2>Resolução da equação:</h2>
                  <br />

                  <span class="span"
                    >{{ diametro_parafuso || "d" }} = √4/π x ({{
                      forca_diametro || "P"
                    }}/{{ tensao_adm || "σ_adm" }})</span
                  ></v-card-text
                >
              </v-card-text>
            </v-card>
          </v-dialog>
          <!-- /Modal diametro-->
        </div>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <div class="text-center">
          <!-- Modal Espessura-->
          <v-dialog v-model="dialog_espessura" width="500">
            <v-card>
              <v-card-title style="background: #d71c23; color: white">
                Equação para espessura do teto</v-card-title
              >
              <v-card-text class="pa-5" style="color: #000">
                <h3 class="mb-5">h = 1/(π x d_arruela) x (P/τ_cisalhamento)</h3>
                <v-text-field
                  v-model="forca_espessura"
                  suffix="N"
                  label="Força"
                ></v-text-field>
                <v-text-field
                  suffix="m"
                  label="Diâmetro da arruela"
                  v-model="diametro_arruela"
                ></v-text-field>
                <v-text-field
                  suffix="Pa"
                  label="Tensão de cisalhamento do material (parte superior)"
                  v-model="tensao_cisalhamento"
                ></v-text-field>
                <v-text-field
                  readonly
                  suffix="mm"
                  label="Resposta - Espessura mínima do teto"
                  v-model="espessura_teto"
                ></v-text-field>

                <div class="mb-7">
                  <v-btn
                    @click="limpar_espessura"
                    color="red"
                    class="mr-3 white--text"
                    >Limpar Campos</v-btn
                  >
                  <v-btn @click="calcular_espessura" color="primary"
                    >Calcular</v-btn
                  >
                </div>

                <v-card-text>
                  <h2>Resolução da equação:</h2>
                  <br />
                  <span class="span">
                    {{ espessura_teto || "h" }} = 1/(π x
                    {{ diametro_arruela || "d_arruela" }}) x ({{
                      forca_espessura || "P"
                    }}/{{ tensao_cisalhamento || "τ_cisalhamento" }})
                  </span>
                </v-card-text>
              </v-card-text>
            </v-card>
          </v-dialog>
          <!-- /Modal Espessura-->
        </div>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      dialog_diametro: "",
      dialog_espessura: "",
      forca_diametro: "",
      tensao_adm: "",
      diametro_parafuso: "",
      forca_espessura: "",
      diametro_arruela: "",
      tensao_cisalhamento: "",
      espessura_teto: "",
    };
  },
  methods: {
    calcular_diametro() {
      let forca = this.forca_diametro;
      let tensao_adm = this.tensao_adm;
      let diametro_parafuso = Math.sqrt((4 / Math.PI) * (forca / tensao_adm));
      let diametroMM = (diametro_parafuso * 1000).toFixed(2);
      this.diametro_parafuso = diametroMM;
    },
    calcular_espessura() {
      let forca = this.forca_espessura;
      let diametro_arruela = this.diametro_arruela;
      let tensao_cisalhamento = this.tensao_cisalhamento;
      let espessura =
        (1 / (Math.PI * diametro_arruela)) * (forca / tensao_cisalhamento);
      let espessuraMM = (espessura * 1000).toFixed(2);
      this.espessura_teto = espessuraMM;
    },
    limpar_diametro() {
      this.forca_diametro = "";
      this.tensao_adm = "";
      this.diametro_parafuso = "";
    },
    limpar_espessura() {
      this.forca_espessura = "";
      this.diametro_arruela = "";
      this.tensao_cisalhamento = "";
      this.espessura_teto = "";
    },
  },
};
</script>

<style scoped>
span.span {
  font-size: 17px;
  color: grey;
}
</style>