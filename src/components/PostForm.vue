<script>
export default {
  props: {
    post: Object,
    id: Number,
  },
  data() {
    return {
      formData: {
        title: this.post?.title || "",
        content: this.post?.content || "",
      },
      isEditable: Boolean(this.post),
      tituloForm: Boolean(this.post) == true ? "Editar Post": "Criar novo Post" 
    };
  },
  methods: {
    handlePost(post) {
      if (!this.formData.title || !this.formData.content) {
        alert("Faltou preencher alguma informação do post");
        return;
      }

      const dataDaPostagem = this.createDatetime();

      const thePost = {
        datetime: dataDaPostagem,
        ...this.formData,
      };

      if (this.isEditable == true) {
        this.$emit("edit-post", thePost, this.id);
      } else {
        this.$emit("create-post", thePost);
      }

      this.formData = {};

      this.$router.push("/");
    },
    createDatetime() {
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

      const datetime = date + " - " + hour;

      return datetime;
    },
  },
};
</script>

<template>
  <h2 class="fSizeLarge">{{ tituloForm }}</h2>
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

<style scoped>
  h2 {
    text-align: center;
    margin: 2rem;
  }
</style>