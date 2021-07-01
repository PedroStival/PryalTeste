<template>
  <div id="style-4">
    <div className="card card-custom">
      <div className="card-header border-0">
        <h3 className="card-title font-weight-bolder text-dark">
          Pré-Cadastro de Laudos
        </h3>
        <div className="card-toolbar">
          <button
            className="btn btn-primary font-weight-bolder font-size-sm mr-3 d-flex"
          >
            Cadastrar
          </button>
        </div>
      </div>
      <div className="card-body pt-2" v-for="cliente in clientes" :key="cliente.id">
        <div className="d-flex flex-wrap align-items-center">
          <div className="d-flex flex-column flex-grow-1 my-lg-0 my-2 pr-3">
            <span class="fs-3">Cliente: {{ cliente.nome }}</span>
            <template v-for="veiculo in cliente.veiculos" :key="veiculo.id">
            <span
              className="d-flex align-items-center justify-content-between text-muted mb-3"
            >
              <span className="font-size-sm">
                {{veiculo.marca}} {{veiculo.modelo}} | Placa {{veiculo.placa}}
              </span>
              <button class="btn btn-sm btn-info" @click="criarLaudo(veiculo.id)">Criar laudo</button>
            </span>
            </template>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import ApiService from "@/core/services/ApiService"
import { useRouter } from "vue-router"

export default defineComponent({
  name: "ClientesList",
  components: {},
  props: {
      clientes: Array
  },
  setup() {
      const router = useRouter();
      function criarLaudo(veiculoId) {
          ApiService.post("/analise/cadastrar?veiculoId=" + veiculoId, {}).then(({ data }) => {
              router.push({ name: "Cadastrar-laudo", params: { analiseId: data }})
          });
      }
      
      return {
          criarLaudo
      }
  }
});
</script>
