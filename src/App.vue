<script>
import { RouterLink, RouterView } from "vue-router";
import "@/assets/css/base.css";

export default {
  data() {
    return {
      posts: [],
    };
  },
  methods: {
    addPost(newPost) {
      this.posts.push(newPost);
    },
  },
};
</script>

<template>
  <header>
    <RouterLink to="/">Home</RouterLink>
  </header>

  <main>
    <RouterView :posts="posts" @create-post="addPost" />
  </main>

  <footer>
    <RouterLink to="/create">Novo Post</RouterLink>
  </footer>
</template>

<style scoped></style>
