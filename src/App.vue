<script>
import { RouterLink, RouterView } from "vue-router";

export default {
  data() {
    return {
      posts: [],
      formData: {},
      search: "",
    };
  },
  computed: {
    filteredPosts() {
      if(!this.search) return this.posts;

      const listaFinal = [];
      for (const post of this.posts) {
        if(post.title.includes(this.search)) {
          listaFinal.push(post);
        }
      }
      return listaFinal;
    }
  },
  methods: {
    handleSubmit(event) {
      event.preventDefault();

      const now = new Date();

      const dataDaPostagem = `${now.getDate()}/${now.getMonth()}/${now.getFullYear()} - ${now.getHours()}:${now.getMinutes()}`;

      this.posts.push({
        title: this.formData.title,
        content: this.formData.content,
        datetime: dataDaPostagem,
      });

      this.formData = {};
    },
    handleInputChange(event) {
      const { name, value } = event.target;
      this.formData[name] = value;
    },
  },
};
</script>

<template>
  <header></header>

  <input class="busca search" type="text" v-model="search" placeholder="Procurar">

  <div id="list-posts">
    <div class="post" v-for="post in filteredPosts" :key="post.title">
      <h3>{{ post.title }}</h3>
      <h4>{{ post.datetime }}</h4>
      <p>{{ post.content }}</p>
    </div>
  </div>

  <form action="" @submit="handleSubmit">
    <input placeholder="Titulo" v-model="formData.title" />
    <textarea
      :value="formData.content"
      name="content"
      @keyup="handleInputChange"
      placeholder="Escreva seu post aqui"
      cols="30"
      rows="10"
    ></textarea>
    <button class="submit" type="submit">Salvar</button>
  </form>

  <main>
    <RouterView />
  </main>

  <footer></footer>
</template>

<style scoped>
.search {
  position: fixed;
  right: 45%;
  z-index: 1;
  padding: 1rem;
}
h3, h4, p, input, textarea {
  font-family: sans-serif;
  margin: 0;
  color: #1a1a1a;
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

form {
  display: flex;
  flex-direction: column;
  position: fixed;
  top: 0;
  left: 1rem;
  width: 25vw;
}

form > * {
  margin: 1rem 0;
  padding: 1rem;
  font-size: 1rem;
}

textarea, p {
  line-height: 1.5rem;
}

textarea {
  resize: none;
}

.submit {
  width: 100px;
  margin: auto;
  border: none;
  background-color: #1a1a1a;
  color: #fff;
  cursor: pointer;
  transition: all ease 0.3s;
}

.submit:hover {
  opacity: 0.8;
}
</style>
