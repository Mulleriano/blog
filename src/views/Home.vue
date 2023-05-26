<script>
import { RouterLink } from "vue-router";
export default {
  data() {
    return {
      search: "",
      showModal: false,
      postId: null,
      postTitle: null,
    };
  },
  props: {
    posts: Array,
    search: String,
  },
  computed: {
    filteredPosts() {
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
    toggleModal(id, title) {
      this.showModal = !this.showModal;
      /* Alimenta a variável de id */
      this.postId = id;
      this.postTitle = title;
    },
    deletePost() {
      this.$emit("delete-post", this.postId);
      this.showModal = !this.showModal;
    },
  },
};
</script>

<template>
  <div id="list-posts">
    <div class="post" v-for="post in filteredPosts" :key="post.title">
      <!--       <div class="actions"> -->
      <RouterLink title="Editar" :to="`/edit/${getPostId(post.title)}`">
        <span class="material-symbols-rounded details"> edit </span>
      </RouterLink>
      <span
        title="Deletar"
        @click="toggleModal(getPostId(post.title), post.title)"
        class="material-symbols-rounded delete deletar"
      >
        delete
      </span>
      <!--       </div> -->
      <RouterLink :to="`/detail/${getPostId(post.title)}`">
        <h3>
          {{ post.title }}
        </h3>
      </RouterLink>
      <h4>{{ post.datetime }}</h4>
      <p>{{ post.content }}</p>
    </div>
  </div>

  <div class="modal center" v-show="showModal">
    <div class="modal-content">
      <h3>Deletar</h3>
      <p>Tem certeza que quer deletar o post "{{ postTitle }}"?</p>

      <button @click="toggleModal" class="redButton">Cancelar</button>
      <button @click="deletePost">Confirmar</button>
    </div>
  </div>
</template>

<style scoped>
#list-posts {
  margin: auto;
  max-width: 1024px;
  padding: 0 2rem 1rem 2rem;
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

.details,
.deletar {
  z-index: 1;
  cursor: pointer;
  position: absolute;
  right: 1rem;
}

.details {
  right: 3rem;
}

/* .actions {
  display: flex;
  text-align: center;
  position: absolute;
  right: 1rem;
  top: 1rem;
  cursor: pointer;
  z-index: 1;
} */

.options > * {
  margin-left: 5px;
}
</style>
