<script>
export default {
  data() {
    return {
      formData: {},
    };
  },
  methods: {
    handleClick(event) {
      event.preventDefault();
      if(!this.formData.title || !this.formData.content) {
        alert("Faltou preencher alguma informação do post");
        return;
      }

      const now = new Date();
      const date =
        ('0'+ now.getDate()).slice(-2) + '/' + // Dia
        ('0' + now.getMonth()).slice(-2) + '/' + // Mês
        now.getFullYear(); // Ano

      const hour =
        ('0' + now.getHours()).slice(-2) + ':' + // Horas
        ('0' + now.getMinutes()).slice(-2); // Minutos

      const dataDaPostagem = date + ' - ' + hour;

      const newPost = {
        title: this.formData.title,
        content: this.formData.content,
        datetime: dataDaPostagem,
      };

      this.$emit("create-post", newPost);

      this.formData = {};

      this.$router.push("/")
    },
  },
};
</script>

<template>
  <form action="">
    <input placeholder="Titulo" v-model="formData.title" />
    <textarea
      v-model="formData.content"
      placeholder="Escreva seu post aqui"
      cols="30"
      rows="10"
    ></textarea>
    <button class="submit" type="submit" @click="handleClick">Salvar</button>
  </form>
</template>

<style scoped></style>
