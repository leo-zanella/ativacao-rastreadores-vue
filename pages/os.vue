<template>
  <v-stepper v-model="e1" alt-labels>
    <v-stepper-header>
      <v-stepper-step :complete="e1 > 1" step="1" class="custom-complete-icon">
        Antes de instalar
      </v-stepper-step>

      <v-divider></v-divider>

      <v-stepper-step :complete="e1 > 2" step="2">
        Informações para ativação
      </v-stepper-step>

      <v-divider></v-divider>

      <v-stepper-step :complete="e1 > 3" step="3">
        Testes para ativação
      </v-stepper-step>

      <v-divider></v-divider>

      <v-stepper-step :complete="e1 > 4" step="4">
        Após instalação
      </v-stepper-step>

      <v-divider></v-divider>

      <v-stepper-step step="5"> </v-stepper-step>
    </v-stepper-header>

    <v-stepper-items>
      <v-stepper-content step="1">
        <h2 class="d-flex justify-center align-center">
          Check-list pré instalação
        </h2>
        <v-form ref="form" class="fill-height align-center">
          <v-row class="flex-column align-center mt-4">
            <v-card-subtitle class="font-weight-medium" font-size
              >Estado da fiação do veículo:</v-card-subtitle
            >
            <v-col cols="12" sm="4">
              <v-select :items="estado" label="Selecione uma opção"></v-select>
            </v-col>

            <v-card-subtitle class="font-weight-medium"
              >Estado da bateria do veículo:</v-card-subtitle
            >
            <v-col class="d-flex" cols="12" sm="4">
              <v-select :items="estado" label="Selecione uma opção"></v-select>
            </v-col>

            <v-col class="d-flex" cols="12" sm="4">
              <ChecklistTeste @dados-checkbox="atualizarDadosCheckbox" />
            </v-col>
          </v-row>

          <div class="mb-5 d-flex justify-end">
            <v-btn
              dark
              class="mb-7"
              color="green darken-2"
              :disabled="exibirOverlay"
              @click="avancarSemOverlay" 
            >
              Confirmar
            </v-btn>
          </div>
        </v-form>

        <v-overlay :value="exibirOverlay" @input="fecharOverlay">
          <v-card class="pa-4">
            <div>
              Avise o cliente que a(s) seguinte(s) peças do veículo não estão
              funcionando: {{ checkboxesNaoMarcadosTexto }}.
            </div>
            <v-btn color="primary" @click="fecharOverlay">Confirmar</v-btn>
          </v-card>
        </v-overlay>
      </v-stepper-content>

      <v-stepper-content step="2">
        <div id="step2">
          <h2 class="d-flex justify-center align-center">
            Dados da instalação
          </h2>

          <v-form ref="form" class="fill-height d-flex align-center">
            <v-row class="flex-column align-center">
              <v-card-subtitle class="mt-10">Rastreador:</v-card-subtitle>
              <v-col cols="12" md="4">
                <v-text-field
                  :counter="max"
                  label="Código do rastreador"
                ></v-text-field>
              </v-col>
              <div class="text-center">
                <v-dialog v-model="dialog" width="500">
                  <template #activator="{ on, attrs }">
                    <v-btn color="grey darken-3" dark v-bind="attrs" v-on="on">
                      Clique para saber qual é o código
                    </v-btn>
                  </template>

                  <v-card>
                    <v-card-title class="text-h5 grey lighten-2">
                      Onde está o código?
                    </v-card-title>
                    <v-img
                      rounded-lg
                      classbr="10"
                      :src="require('../static/maxtrack.png')"
                    ></v-img>

                    <v-divider></v-divider>

                    <v-card-actions>
                      <v-spacer></v-spacer>
                      <v-btn color="primary" text @click="dialog = false">
                        Entendi
                      </v-btn>
                    </v-card-actions>
                  </v-card>
                </v-dialog>
              </div>

              <v-col cols="12" md="4">
                <v-text-field
                  v-model="localinstalacao"
                  label="Local de fixação do rastreador"
                ></v-text-field>
              </v-col>

              <v-card-subtitle class="mt-10">Veículo:</v-card-subtitle>

              <v-col cols="12" md="4">
                <v-text-field
                  v-model.lazy="placa"
                  label="Placa do veículo"
                  @blur="validarPlaca"
                ></v-text-field>
                <v-alert v-if="placa == null" dense type="error"
                  >PLACA INVÁLIDA</v-alert
                >
              </v-col>

              <v-col class="d-flex" cols="12" sm="4">
                <v-select
                  :items="bloqueio"
                  label="O veículo possui chave geral?"
                ></v-select>
              </v-col>
              <v-card-subtitle class="mt-10">Anexos:</v-card-subtitle>
              <v-col class="d-flex align-center" cols="12" sm="4">
                <v-file-input
                ref="fileInputPlaca"
                  v-model="placaAnexo"
                  label="Placa do veículo"
                  prepend-icon="mdi-camera"
                  accept="image/*"
                  capture
                  @change="handleFileInputChange('placaAnexo')"
                ></v-file-input>
              </v-col>

              <v-col class="d-flex align-center" cols="12" sm="4">
                <v-file-input
                ref="fileInputCodigoRastreador"
                  v-model="codigoRastreadorAnexo"
                  label="Código do rastreador"
                  prepend-icon="mdi-camera"
                  accept="image/*"
                  capture
                  @change="handleFileInputChange(codigoRastreadorAnexo)"
                ></v-file-input>
              </v-col>

              <v-col class="d-flex align-center" cols="12" sm="4">
                <v-file-input
                ref="fileInputPositivo"
                  v-model="positivoAnexo"
                  label="Positivo"
                  prepend-icon="mdi-camera"
                  accept="image/*"
                  capture
                  @change="handleFileInputChange(positivoAnexo)"
                ></v-file-input>
              </v-col>

              <v-col class="d-flex align-center" cols="12" sm="4">
                <v-file-input
                ref="fileInputCodigoNegativo"
                  v-model="negativoAnexo"
                  label="Negativo"
                  prepend-icon="mdi-camera"
                  accept="image/*"
                  capture
                  @change="handleFileInputChange(negativoAnexo)"
                ></v-file-input>
              </v-col>

              <v-col class="d-flex align-center" cols="12" sm="4">
                <v-file-input
                ref="fileInputCodigoFixado"
                  v-model="rastreadorFixadoAnexo"
                  label="Rastreador fixado no veículo"
                  prepend-icon="mdi-camera"
                  accept="image/*"
                  capture
                  @change="handleFileInputChange(rastreadorFixadoAnexo)"
                ></v-file-input>
              </v-col>
            </v-row>
          </v-form>

          <div class="mt-10 mb-10 d-flex justify-end">
            <v-btn text @click="e1 = 1"> Voltar </v-btn>
            <v-btn dark color="green darken-2" @click="confirmarStep">
              Confirmar
            </v-btn>
          </div>
        </div>
      </v-stepper-content>

      <v-stepper-content step="3">
        <AtivacaoRastreador />

        <div class="mb-10 mt-5 d-flex justify-end">
          <v-btn text @click="e1 = 2"> Voltar </v-btn>

          <v-btn dark color="green darken-2" @click="confirmarStep">
            Confirmar
          </v-btn>
        </div>
      </v-stepper-content>

      <v-stepper-content step="4">
        <h2 class="d-flex justify-center align-center">
          Check-list pós instalação
        </h2>
        <v-form ref="form" class="fill-height align-center">
          <v-row class="flex-column align-center mt-4">
            <v-col class="d-flex" cols="12" sm="4">
              <ChecklistTeste @dados-checkbox="atualizarDadosCheckbox" />
            </v-col>
          </v-row>

          <div class="d-flex justify-end">
            <v-btn text @click="e1 = 3"> Voltar </v-btn>
            <v-btn
              dark
              class="mb-7"
              color="green darken-2"
              @click="confirmarStep"
            >
              Confirmar
            </v-btn>
          </div>
        </v-form>
      </v-stepper-content>

      <v-stepper-content step="5">
        <v-container class="d-flex flex-column align-center justify-center">
          <v-card-title>Assinatura</v-card-title>
          <v-divider></v-divider>

          <v-col cols="12" sm="4">
            <v-card-subtitle class="mt-8 subtitle-1 align-left"
              >Resposável da frota:</v-card-subtitle
            >

            <v-text-field label="Nome completo"></v-text-field>

            <v-text-field v-mask="'###.###.###-##'" label="CPF"></v-text-field>

            <assinaturaDigital />

            <v-card-subtitle class="mt-8 subtitle-1 align-left"
              >Técnico instalador:</v-card-subtitle
            >

            <v-text-field
              class="mt-5"
              label="Nome completo do técnico instalador"
            ></v-text-field>
          </v-col>
        </v-container>
        <div class="d-flex justify-end">
          <v-btn text @click="e1 = 4"> Voltar </v-btn>
          <v-btn dark color="green darken-2" @click="e1 = 1"> Confirmar </v-btn>
        </div>
      </v-stepper-content>
    </v-stepper-items>
  </v-stepper>
</template>
  
  <script>
import AtivacaoRastreador from '../components/ativacaoRastreadores.vue'
import ChecklistTeste from '../components/ChecklistTeste.vue'
import assinaturaDigital from '@/components/assinaturaDigital.vue'

export default {

  components: {
    ChecklistTeste,
    AtivacaoRastreador,
    assinaturaDigital,
  },

  data() {
    return {
      e1: 1,
      estado: ['Boa', 'Regular', 'Ruim'],
      bloqueio: ['Sim', 'Não'],
      localinstalacao: '',
      allowSpaces: false,
      match: '',
      max: 10,
      dialog: false,
      placa: '',
      checkboxes: [],
      exibirOverlay: false,
      placaAnexo: null,
      codigoRastreadorAnexo: null,
      positivoAnexo: null,
      negativoAnexo: null,
      rastreadorFixadoAnexo: null,
    }
  },


  methods: {
    formatCPF() {
      // Remove todos os caracteres não numéricos
      this.cpf = this.cpf.replace(/\D/g, '')

      // Formata o CPF: XXX.XXX.XXX-XX
      if (this.cpf.length > 3) {
        this.cpf = this.cpf.replace(/^(\d{3})(.*)/, '$1.$2')
      }
      if (this.cpf.length > 6) {
        this.cpf = this.cpf.replace(/^(\d{3})\.(\d{3})(.*)/, '$1.$2.$3')
      }
      if (this.cpf.length > 9) {
        this.cpf = this.cpf.replace(
          /^(\d{3})\.(\d{3})\.(\d{3})(.*)/,
          '$1.$2.$3-$4'
        )
      }
    },

    validarPlaca() {
      // Remover hífen e converter para letras maiúsculas
      const placaSemHifen = this.placa.replace('-', '', 4).toUpperCase()

      if (this.validarPlacaFormato(placaSemHifen)) {
        if (placaSemHifen.length === 7) {
          // Adicionar hífen no padrão antigo (AAA1234)
          this.placa = `${placaSemHifen.slice(0, 3)}-${placaSemHifen.slice(3)}`
        } else if (placaSemHifen.length === 8) {
          // Remover hífen no padrão Mercosul (AAA1A23)
          this.placa = `${placaSemHifen.slice(0, 3)}${placaSemHifen.slice(4)}`
        }
      } else {
        this.placa = null
      }
    },

    validarPlacaFormato(placa) {
      const regexPlacaAntiga = /^[A-Z]{3}\d{4}$/ // Padrão antigo: AAA1234
      const regexPlacaMercosul = /^[A-Z]{3}\d[A-Z0-9]\d{2}$/ // Padrão Mercosul: AAA1A23

      return regexPlacaAntiga.test(placa) || regexPlacaMercosul.test(placa)
    },

    atualizarDadosCheckbox(dados) {
      this.checkboxes = dados.map((item) => item.checked || false)
    },

    fecharOverlay() {
      if (this.exibirOverlay) {
        this.exibirOverlay = false
        this.confirmarStep()
      }
    },

    avancarSemOverlay() {
      const todosMarcados = this.checkboxes.some((checkbox) => !checkbox)
      if (todosMarcados) {
        this.exibirOverlay = true
      } else {
        this.confirmarStep()
      }
    },

    confirmarStep() {
      if (this.$refs.form.validate()) {
    this.e1 = this.e1 + 1;
    window.scrollTo({ top: 0, behavior: 'smooth' });
  } else {
    // Se algum campo não for válido, exiba uma mensagem de erro
    this.$snackbar.showSnackbar({
      text: 'Por favor, preencha todos os campos obrigatórios.',
      color: 'error',
    });
  }
    },

    handleFileInputChange(fieldName) {
      const fileInputRef =
        fieldName === 'placaAnexo'
          ? this.$refs.fileInputPlaca
          : this.$refs.fileInputCodigoRastreador
      const selectedFile = fileInputRef.files[0]

      // Verifica se um arquivo foi selecionado e atualiza o valor correspondente
      if (selectedFile) {
        this[fieldName] = selectedFile
      } else {
        // Se nenhum arquivo for selecionado, redefine o valor correspondente para uma string vazia
        this[fieldName] = ''
      }
    },

    computed: {
      checkboxesNaoMarcadosTexto() {
        const checkboxesNaoMarcados = this.checkboxes.filter(
          (checkbox) => !checkbox
        )
        return checkboxesNaoMarcados
          .map((checkbox) => checkbox.label)
          .join(', ')
      },
    },

    watch: {
      checkboxes: {
        deep: true,
        handler() {
          if (this.podeAvancar && this.exibirOverlay) {
            this.exibirOverlay = false
          }
        },
      },
    },
  },
}
</script>
  
  <style scoped>
.v-card__subtitle,
.v-card__text,
.v-card__title {
  padding: 0px;
  font-size: 18px;
}

.campoinfo {
  margin: 15px;
  padding: 30px;
}

.v-card > h5 {
  margin: 15px;
}

.v-stepper-step {
  text-align: center;
}
</style>