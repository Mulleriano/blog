<script>
import { RouterLink, RouterView } from "vue-router";
import "@/assets/css/base.css";

export default {
  data() {
    return {
      posts: [],
      search: "",
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
    <input class="search" v-model="search" placeholder="Procurar" />
    <nav>
      <RouterLink to="/create">Novo Post</RouterLink>
    </nav>
  </header>

  <main>
    <RouterView :search="search" :posts="posts" @create-post="addPost" />
  </main>

  <footer></footer>
</template>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 2rem;
  z-index: 1;
  background: #24292f;
  color: #fff;
}


.search {
  padding: 0.5rem;
}

</style>
