<script>
import { RouterLink, RouterView } from "vue-router";
import "@/assets/css/base.css";

export default {
  data() {
    return {
      posts: [
        {
          title: "Post 1",
          content:
            "Lorem ipsum dolor sit, amet consectetur adipisicing elit. Quae nostrum qui, repellendus, accusamus corporis quam itaque iure aspernatur impedit quidem asperiores officia modi temporibus hic molestias sequi quia fuga eligendi.",
          datetime: "24/05/1999 - 10:30",
        },
        {
          title: "Post 2",
          content:
            "Lorem ipsum dolor sit, amet consectetur adipisicing elit. Quae nostrum qui, repellendus, accusamus corporis quam itaque iure aspernatur impedit quidem asperiores officia modi temporibus hic molestias sequi quia fuga eligendi.",
          datetime: "24/05/1999 - 10:30",
        },
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
        <span class="material-symbols-rounded fSizeLarge center"> add </span>
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

@media screen and (max-width: 600px){
  .search {
    right: 47%;
    width: 150px;
  }
}
</style>
