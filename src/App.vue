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
      <RouterLink title="Novo Post" class="fSizeLarge" to="/create">+</RouterLink>
    </nav>
  </header>

  <main>
    <RouterView :search="search" :posts="posts" @create-post="addPost" />
  </main>

  <footer></footer>
</template>

<style scoped>

.search {
  position: fixed;
  right: 50%;
  top: 0.6rem;
  margin: 0;
  border: none;
  transform: translateX(50%);
  padding: 0.5rem;
  border-radius: 5px;
}
.search:focus {
  outline: none;
}

</style>
