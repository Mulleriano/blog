<script>
import { RouterLink, RouterView } from "vue-router";
import "@/assets/css/base.css";

export default {
  data() {
    return {
      posts: [
      ],
      search: "",
    };
  },
  methods: {
    addPost(thePost) {
      this.posts.push(thePost);
    },
    updatePost(thePost, id) {
      this.posts[id] = thePost;
    },
    deletePost(id) {
      this.posts.splice(id, 1);
    },
  },
};
</script>

<template>
  <header>
    <RouterLink to="/">Home</RouterLink>
    <input class="search" v-model="search" placeholder="Procurar" />
    <nav>
      <RouterLink title="Novo Post" to="/create">
        <span class="material-symbols-rounded fSizeLarge"> add </span>
      </RouterLink>
    </nav>
  </header>

  <main>
    <RouterView
      :search="search"
      :posts="posts"
      @create-post="addPost"
      @edit-post="updatePost"
      @delete-post="deletePost"
    />
  </main>

  <footer></footer>
</template>

<style scoped>
.search {
  position: absolute;
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
