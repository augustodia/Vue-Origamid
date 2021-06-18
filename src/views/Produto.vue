<template>
  <section>
    <transition mode="out-in">
      <div v-if="produto" class="produto">
        <ul class="fotos" v-if="produto.fotos">
          <li v-for="(foto, index) in produto.fotos" :key="index">
            <img :src="foto.src" :alt="foto.titulo" />
          </li>
        </ul>
        <div class="info">
          <h2>{{ produto.nome }}</h2>
          <p class="preco">{{ produto.preco | numeroPreco }}</p>
          <p class="descricao">{{ produto.descricao }}</p>
          <button class="btn" v-if="produto.vendido === 'false'">
            Comprar
          </button>
          <button disabled class="btn" v-else>Produto Vendido</button>
        </div>
      </div>
      <pagina-carregando v-else></pagina-carregando>
    </transition>
  </section>
</template>

<script>
import { api } from "@/services.js";

export default {
  name: "Produto",
  props: ["id"],
  data() {
    return {
      produto: null,
    };
  },
  methods: {
    getProduto() {
      setTimeout(() => {
        api.get(`/produto/${this.id}`).then((r) => {
          this.produto = r.data;
        });
      }, 2000);
    },
  },
  created() {
    this.getProduto();
  },
};
</script>

<style scoped>
.produto {
  display: grid;
  grid-template-columns: 1fr;
  grid-gap: 30px;
  max-width: 900px;
  padding: 60px 20px;
  margin: 0 auto;
}

.preco {
  color: #e80;
  font-weight: bold;
  font-size: 1.5rem;
  margin-bottom: 40px;
}

.descricao {
  font-size: 1.2rem;
}

.btn {
  margin-top: 60px;
  width: 200px;
}
</style>
