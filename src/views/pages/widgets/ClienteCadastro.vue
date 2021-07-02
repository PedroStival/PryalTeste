<template>
    <div class="modal fade" tabindex="-1" id="pryal_cliente_cadastro">
        <div class="modal-dialog modal-dialog-centered modal-dialog-scrollable modal-fullscreen-sm-down">
            <div class="modal-content">
            <div class="modal-header">
                <h5 class="modal-title">Cadastro de novo cliente</h5>

                <!--begin::Close-->
                <div
                class="btn btn-icon btn-sm btn-active-light-primary ms-2"
                data-bs-dismiss="modal"
                aria-label="Close"
                >
                <span class="svg-icon svg-icon-2x"></span>
                </div>
                <!--end::Close-->
            </div>

            <div class="modal-body">
                <div class="form-floating mb-3">
                    <input v-model="cadastro.nome" type="text" class="form-control" id="form-nome" placeholder="Nome do Cliente">
                    <label for="form-nome">Nome do Cliente</label>
                </div>
                <div class="form-floating mb-3">
                    <input v-model="cadastro.cpf" type="text" class="form-control" id="form-cpf" placeholder="CPF" v-mask="'###.###.###-##'">
                    <label for="form-cpf">CPF</label>
                </div>
                <div class="form-floating mb-3">
                    <input v-model="cadastro.email" type="email" class="form-control" id="form-email" placeholder="Email">
                    <label for="form-email">Email</label>
                </div>
                <div class="form-floating mb-3">
                    <Field v-model="cadastro.dataDeNascimento" type="date" class="form-control" id="form-dtnascimento" placeholder="Data de Nascimento" />
                    <label for="form-dtnascimento">Data de Nascimento</label>
                </div>
                <div class="form-floating mb-3">
                    <select v-model="cadastro.marca" class="form-select" id="marcas" aria-label="Floating label select example" placeholder="Marca">
                        <option selected></option>
                        <option value="Ford">Ford</option>
                        <option value="Ferrari">Ferrari</option>
                        <option value="3">Three</option>
                    </select>
                    <label for="marcas">Marca</label>
                </div>
                <div class="form-floating mb-3">
                    <input v-model="cadastro.modelo" type="text" class="form-control" id="form-modelo" placeholder="Modelo">
                    <label for="form-modelo">Modelo</label>
                </div>
                <div class="input-group mb-3">
                    <input v-model="cadastro.quilometragem" type="number" class="form-control" placeholder="Quilometragem" aria-label="Quilometragem" aria-describedby="form-quilimetragem">
                    <span class="input-group-text" id="form-quilimetragem">KM</span>
                </div>
                <div class="form-floating mb-3">
                    <input v-model="cadastro.anoFabricacao" type="text" class="form-control" id="form-anofabricacao" placeholder="Ano Fabricação">
                    <label for="form-anofabricacao">Ano Fabricação</label>
                </div>
                <div class="form-floating mb-3">
                    <input v-model="cadastro.anoModelo" type="text" class="form-control" id="form-anomodelo" placeholder="Ano Modelo">
                    <label for="form-anomodelo">Ano Modelo</label>
                </div>
                <div class="form-floating mb-3">
                    <input v-model="cadastro.placa" type="text" class="form-control text-uppercase" id="form-placa" placeholder="Placa" v-mask="'AAA-#X##'">
                    <label for="form-placa">Placa</label>
                </div>
                <div class="form-floating mb-3">
                    <input v-model="cadastro.renavam" type="number" class="form-control" id="form-renavam" placeholder="Renavam">
                    <label for="form-renavam">Renavam</label>
                </div>
                <div class="form-floating mb-3">
                    <input v-model="cadastro.chassi" type="text" class="form-control text-uppercase" id="form-chassi" placeholder="Chassi">
                    <label for="form-chassi">Chassi</label>
                </div>
            </div>

            <div class="modal-footer">
                <button
                type="button"
                class="btn btn-light"
                data-bs-dismiss="modal"
                >
                Fechar
                </button>
                <button type="button" @click="cadastrar" class="btn btn-primary">
                Cadastrar Cliente
                </button>
            </div>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import { saveToken } from "@/core/services/JwtService";
import ApiService from "@/core/services/ApiService";
import Swal from "sweetalert2/dist/sweetalert2.min.js";
import { Field } from "vee-validate";

export default defineComponent({
  name: "ClienteCadastro",
  components: { Field },
  setup() {
      const cadastro = ref({});

      function cadastrar() {
        saveToken(
            "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1bmlxdWVfbmFtZSI6IlBlZHJvIiwicm9sZSI6IkFkbWluaXN0cmFkb3IiLCJuYmYiOjE2MjUwOTk2MzQsImV4cCI6MTY1NjYzNTYzNCwiaWF0IjoxNjI1MDk5NjM0fQ.SFpPm7a5AIKjIkb0rwXIi5DxqI_pjAaNG4XtPw-_VJk"
        );
        ApiService.setHeader();
            ApiService.post("clientes/cadastrar", cadastro.value).then(() => {
                Swal.fire({
                    text: "Cliente foi registrado com sucesso!",
                    icon: "success",
                    buttonsStyling: false,
                    confirmButtonText: "Ok, proximo!",
                    customClass: {
                    confirmButton: "btn fw-bold btn-light-primary"
                    }
                })
            });
      }
      return {
          cadastrar,
          cadastro,
          Field
      }
  }
})
</script>