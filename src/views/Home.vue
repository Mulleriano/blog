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
