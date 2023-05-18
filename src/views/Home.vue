<script>
import { RouterLink } from "vue-router";
export default {
  data() {
    return {
      search: "",
      showMore: false,
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
  methods: {
    getPostId(title) {
      for (const index in this.posts) {
        const post = this.posts[index];

        if (post.title === title) return index;
      }
    },
  },
};
</script>

<template>
  <div id="list-posts">
    <div class="post" v-for="(post, index) in filteredPosts" :key="post.title">
      <div class="actions">
        <RouterLink :to="`/edit/${getPostId(post.title)}`">
        <span class="material-symbols-rounded"> edit </span>
        </RouterLink>
        <a><span class="material-symbols-rounded delete"> delete </span></a>
      </div>
      <h3>
        {{ post.title }}
      </h3>
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
  line-height: 2.1rem;
  margin-right: 3rem;
}

h4 {
  font-weight: 400;
  font-size: 0.9rem;
  color: #727272;
  font-style: italic;
  margin-bottom: 1rem;
}
p,
a {
  color: #24292f;
}
.post {
  position: relative;
  margin-top: 1rem;
  padding: 1rem 2rem;
  border-radius: 5px;
  border: 1px solid #24292f;
}

.actions {
  display: flex;
  text-align: center;
  position: absolute;
  right: 1rem;
  top: 1rem;
  cursor: pointer;
}

.options > * {
  margin-left: 5px;
}
</style>
