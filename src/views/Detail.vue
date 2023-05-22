<script>
import { RouterLink } from "vue-router";

export default {
  data() {
    const id = this.$route.params.id;

    return {
      id: id,
      post: this.posts[id],
    };
  },
  props: {
    posts: Array,
  },
  methods: {
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
    <p>{{ post.content }}</p>
    <div class="actions">
      <RouterLink class="action" :to="`/edit/${id}`">Editar</RouterLink>
      <a class="action deletar" @click="deletePost">Deletar</a>
    </div>
  </div>
</template>

<style scoped>
.post {
  margin: auto;
  max-width: 1024px;
  padding: 2rem 4rem;
}

.actions {
  margin-top: 2rem;
}
.deletar {
  margin-left: 2rem;
  background-color: #e92024;
}
</style>
