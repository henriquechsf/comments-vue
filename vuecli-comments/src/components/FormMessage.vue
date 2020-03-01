<template>
  <div class="form-comentarios form-group">
    <p>
      <input v-model="name" type="text" name="author" class="form-control" placeholder="Nome" />
    </p>
    <p>
      <textarea v-model="message" name="message" class="form-control" placeholder="Comentário"></textarea>
    </p>
    <button v-on:click="addComment" type="submit" class="btn btn-primary">Comentar</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // dados v-model
      name: "",
      message: ""
    };
  },
  methods: {
    addComment() {
      // validação de campo vazio
      if (this.message.trim() === "") {
        alert("Digite a mensagem!");
        return;
      }

      this.$emit("add-message", {
        name: this.name,
        message: this.message
      });

      this.name = "";
      this.message = "";
    }
  }
};
</script>