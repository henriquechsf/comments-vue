<template>
  <div class="container">
    <h1>Comentários</h1>
    <hr />

    <FormMessage v-on:add-message="addComment" />

    <div class="list-group">
      <p v-if="comments.length <=0">
        <strong>Sem comentários</strong>
      </p>

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
import FormMessage from "./FormMessage";

export default {
  components: {
    FormMessage
  },
  // dados que podemos renderizar na tela {{  }}
  data() {
    return {
      comments: []
    };
  },
  // metodos do componente
  methods: {
    addComment(comment) {
      this.comments.push(comment);
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