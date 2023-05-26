<script>
import { RouterLink } from "vue-router";

export default {
  data() {
    const id = this.$route.params.id;

    return {
      id: id,
      post: this.posts[id],
      showModal: false,
    };
  },
  props: {
    posts: Array,
  },
  methods: {
    toggle() {
      this.showModal = !this.showModal;
    },
    deletePost() {
      this.$emit("delete-post", this.id);
      this.$router.push("/");
    },
  },
};
</script>

<template>
  <div class="post">
    <h3>
      {{ post.title }}
    </h3>
    <h4>{{ post.datetime }}</h4>
    <p class="content">{{ post.content }}</p>
    
    <RouterLink class="action" :to="`/edit/${id}`">Editar</RouterLink>
    <a class="action redButton" @click="toggle">Deletar</a>
  </div>

  <div class="modal center" v-show="showModal">
    <div class="modal-content">
      <h3>Deletar</h3>
      <p>Tem certeza que quer deletar o post "{{ post.title }}"?</p>

      <button @click="toggle" class="redButton">Cancelar</button>
      <button @click="deletePost">Confirmar</button>
    </div>
  </div>
</template>

<style scoped>
.post {
  margin: auto;
  max-width: 1024px;
  padding: 2rem 4rem;
}

.content {
  margin-bottom: 2rem;
}

.action {
  margin-right: 2rem;
  margin-top: 4rem;
}
</style>
