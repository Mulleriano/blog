<script>
export default {
  props: {
    post: Object,
  },
  data() {
    return {
      formData: {
        title: this.post?.title || "",
        content: this.post?.content || "",
      },
    };
  },
  methods: {
    handlePost(post) {

    },
    handleCreatePost(event) {
      if (!this.formData.title || !this.formData.content) {
        alert("Faltou preencher alguma informação do post");
        return;
      }

      const now = new Date();
      const date =
        ("0" + now.getDate()).slice(-2) +
        "/" + // Dia
        ("0" + now.getMonth()).slice(-2) +
        "/" + // Mês
        now.getFullYear(); // Ano

      const hour =
        ("0" + now.getHours()).slice(-2) +
        ":" + // Horas
        ("0" + now.getMinutes()).slice(-2); // Minutos

      const dataDaPostagem = date + " - " + hour;

      const newPost = {
        title: this.formData.title,
        content: this.formData.content,
        datetime: dataDaPostagem,
      };

      this.$emit("create-post", newPost);

      this.formData = {};

      this.$router.push("/");
    },
    handleEditPost(event) {
      if (!this.formData.title || !this.formData.content) {
        alert("Você não pode apagar as informações por completo");
        return;
      }

      const now = new Date();
      const date =
        ("0" + now.getDate()).slice(-2) +
        "/" + // Dia
        ("0" + now.getMonth()).slice(-2) +
        "/" + // Mês
        now.getFullYear(); // Ano

      const hour =
        ("0" + now.getHours()).slice(-2) +
        ":" + // Horas
        ("0" + now.getMinutes()).slice(-2); // Minutos

      const dataDaPostagem = date + " - " + hour;

      const newPost = {
        title: this.formData.title,
        content: this.formData.content,
        datetime: dataDaPostagem,
      };

      const id = 

      this.$emit("updatePost", newPost, id);

      this.formData = {};

      this.$router.push("/");
    },
  },
};
</script>

<template>
  <form>
    <input class="fSizeLarge" placeholder="Titulo" v-model="formData.title" />
    <textarea
      v-model="formData.content"
      placeholder="Escreva seu post aqui"
      cols="30"
      rows="10"
    ></textarea>
    <button class="submit" type="button" @click="handlePost">Salvar</button>
  </form>
</template>
