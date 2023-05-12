<script>
import { RouterLink, RouterView } from "vue-router";

export default {
  data() {
    return {
      posts: [
        {
          title: "Titulo",
          datetime: Date.now(),
          content: "Conteúdo do primeiro post",
        },
        {
          title: "Titulo2",
          datetime: Date.now(),
          content: "Conteúdo do segundo post",
        },
      ],
    };
  },
  methods: {
    handleSubmit(event) {
      event.preventDefault()
    }
  }
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
    <input name="title" />
    <textarea name="content" cols="30" rows="10"></textarea>
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
