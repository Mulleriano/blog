<script>
export default {
  data() {
    return {
      search: "",
    };
  },
  props: {
    posts: Array,
    search: String,
  },
  computed: {
    filteredPosts() {
      console.log(this.$props.search);
      if (!this.$props.search) return this.$props.posts;

      const listaFinal = [];
      for (const post of this.$props.posts) {
        if (post.title.includes(this.$props.search)) {
          listaFinal.push(post);
        }
      }
      return listaFinal;
    },
  },
};
</script>

<template>
  <div id="list-posts">
    <div class="post" v-for="post in filteredPosts" :key="post.title">
      <h3>{{ post.title }}</h3>
      <h4>{{ post.datetime }}</h4>
      <p>{{ post.content }}</p>
    </div>
  </div>
</template>

<style scoped>
#list-posts {
  margin: auto;
  max-width: 1024px;
  padding: 0 2rem 1rem 2rem;
}

h3 {
  color: #24292f;
  font-size: 2rem;
}

h4 {
  font-weight: 400;
  font-size: 0.9rem;
  color: #727272;
  font-style: italic;
  margin-bottom: 1rem;
  margin-top: 10px;
}
p {
  color: #24292f;
}
.post {
  position: relative;
  margin-top: 2rem;
  padding: 1rem 2rem;
  border-radius: 5px;
  border: 1px solid #24292f;
}
</style>
