<template>
  <div className="row">
    <div className="col-lg-6">
      <ClientesList :clientes="clientes" />
    </div>
    <div className="col-lg-6">
      oi oiii
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted, computed } from "vue";
import ClientesList from "@/views/pages/widgets/ClientesList.vue";
import { saveToken } from "@/core/services/JwtService"
import ApiService from "@/core/services/ApiService"

export default defineComponent({
  name: "Dashboard",
  components: { ClientesList },
  setup() {
    const clientes = ref([
      {
        nome: "Pedro"
      }
    ])

    onMounted(() => {
      saveToken("eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1bmlxdWVfbmFtZSI6IlBlZHJvIiwicm9sZSI6IkFkbWluaXN0cmFkb3IiLCJuYmYiOjE2MjUwOTk2MzQsImV4cCI6MTY1NjYzNTYzNCwiaWF0IjoxNjI1MDk5NjM0fQ.SFpPm7a5AIKjIkb0rwXIi5DxqI_pjAaNG4XtPw-_VJk");
      ApiService.setHeader();
      ApiService.get("clientes/listar").then(({ data }) => {
          clientes.value = data;
        });
    })

    return {
      ClientesList,
      clientes
    };
  }
});
</script>
