<template>
  <div class="container">
    <h1>Comentários</h1>
    <hr />
    <div class="form-comentarios form-group">
      <p>
        <input v-model="name" type="text" name="author" class="form-control" placeholder="Nome" />
      </p>
      <p>
        <textarea v-model="message" name="message" class="form-control" placeholder="Comentário"></textarea>
      </p>
      <button v-on:click="addComment" type="submit" class="btn btn-primary">Comentar</button>
    </div>

    <div class="list-group">
      <div class="list-group-item" v-for="(comment, index) in allComments" v-bind:key="index">
        <span class="coment-author">
          Autor:
          <strong>{{ comment.name }}</strong>
        </span>
        <p>{{ comment.message }}</p>
        <div>
          <a href="#" title="Excluir" v-on:click.prevent="removeComment(index)">Excluir</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  // dados que podemos renderizar na tela {{  }}
  data() {
    return {
      comments: [],
      // dados v-model
      name: "",
      message: ""
    };
  },
  // metodos do componente
  methods: {
    addComment() {
      // validação de campo vazio
      if (this.message.trim() === "") {
        alert("Digite a mensagem!");
        return;
      }

      // adiciona os comentários no array comments em data()
      this.comments.push({
        name: this.name,
        message: this.message
      });
      this.name = "";
      this.message = "";
    },

    removeComment(index) {
      this.comments.splice(index);
    }
  },
  // valores computados (lógica para a interface)
  computed: {
    // retorna todos os comentários e retorna 'Anonimo' caso não tenha nome
    allComments() {
      return this.comments.map(comment => ({
        ...comment,
        name: comment.name.trim() === "" ? "Anônimo" : comment.name
      }));
    }
  },
  // monitora alterações nas propriedades
  watch: {
    comments(val) {
      console.log("val", val);
    }
  }
};
</script>