<script>
import { RouterLink, RouterView } from "vue-router";

export default {
  data() {
    return {
      posts: [
        {
          title: "",
          datetime: "",
          content: "",
        },
      ],
      formData: {
        title: "",
        content: "",
      },
    };
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

  <div id="list-posts">
    <div class="post" v-for="post in posts" :key="post.title">
      <h3>{{ post.title }}</h3>
      <h4>{{ post.datetime }}</h4>
      <p>{{ post.content }}</p>
    </div>
  </div>

  <form action="" @submit="handleSubmit">
    <input
      :value="formData.title"
      placeholder="Titulo"
      name="title"
      @keyup="handleInputChange"
      required
      oninvalid="this.setCustomValidity('Ei! Faltou o título')"
    />
    <textarea
      :value="formData.content"
      placeholder="Escreva seu post aqui"
      name="content"
      @keyup="handleInputChange"
      cols="30"
      rows="10"
      required
      oninvalid="this.setCustomValidity('Você precisa escrever seu post')"
    ></textarea>
    <button type="submit">Criar</button>
  </form>

  <main>
    <RouterView />
  </main>

  <footer></footer>
</template>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}

form > * {
  margin: 1rem 0;
}
</style>
