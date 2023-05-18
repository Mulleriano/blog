<script>
import { RouterLink, RouterView } from "vue-router";
import "@/assets/css/base.css";

export default {
  data() {
    return {
      posts: [
        {
          title: "post 1",
          datetime: "24/05/1999 - 10:30",
          content:
            "  Lorem ipsum dolor sit amet consectetur adipisicing elit. Et est suscipit possimus ex rerum repudiandae sunt, quas recusandae inventore delectus optio quia, molestiae alias perspiciatis hic vitae tenetur laudantium velit.",
        },
      ],
      search: "",
    };
  },
  methods: {
    addPost(newPost) {
      this.posts.push(newPost);
    },
    updatePost(updatedPost, id) {
      this.post[id] = updatedPost;
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
