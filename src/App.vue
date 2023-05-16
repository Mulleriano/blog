<script>
import { RouterLink, RouterView } from "vue-router";

export default {
  data() {
    return {
      posts: [
        {
          title: "Titulo 1",
          datetime: Date.now(),
          content: "Lorem ipsum dolor sit amet consectetur, adipisicing elit. Voluptatibus natus, veritatis sed quaerat sint pariatur. Animi amet quidem ad. Maiores iste aperiam velit voluptatibus sint quibusdam quos id ut culpa!",
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
    <button class="submit" type="submit">Salvar</button>
  </form>

  <main>
    <RouterView />
  </main>

  <footer></footer>
</template>

<style scoped>
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
  padding-bottom: 2rem;
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
