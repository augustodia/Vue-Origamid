<template>
  <usuario-form>
    <button class="btn" @click.prevent="atualizarUsuario">
      Atualizar Usuário
    </button>
  </usuario-form>
</template>

<script>
import UsuarioForm from "@/components/UsuarioForm.vue";
import { api } from "@/services.js";
export default {
  components: { UsuarioForm },
  methods: {
    atualizarUsuario() {
      api
        .put(
          `/usuario/${this.$store.state.usuario.id}`,
          this.$store.state.usuario
        )
        .then(() => {
          this.$store.dispatch("getUsuario");
          this.$router.push({ name: "usuario" });
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>

<style></style>
