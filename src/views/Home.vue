<script>
export default {
  data() {
    return {
      search: "",
    };
  },
  props: {
    posts: Array,
  },
  computed: {
    filteredPosts() {
      if (!this.search) return this.posts;

      const listaFinal = [];
      for (const post of this.posts) {
        if (post.title.includes(this.search)) {
          listaFinal.push(post);
        }
      }
      return listaFinal;
    },
  },
};
</script>

<template>
  <input class="search" type="text" v-model="search" placeholder="Procurar" />

  <div id="list-posts">
    <div class="post" v-for="post in filteredPosts" :key="post.title">
      <h3>{{ post.title }}</h3>
      <h4>{{ post.datetime }}</h4>
      <p>{{ post.content }}</p>
    </div>
  </div>
</template>

<style scoped>
.search {
  position: fixed;
  right: 1%;
  z-index: 1;
}

#list-posts {
  position: absolute;
  top: 0;
  right: 50%;
  transform: translateX(50%);
  width: 40vw;
  padding: 2rem 0;
}

h3 {
  font-size: 2rem;
  padding-top: 10px;
  margin-top: 2rem;
}

h4 {
  font-weight: 400;
  color: #727272;
  font-style: italic;
  margin-bottom: 1rem;
}
</style>
