<template>
  <div>
    <h1 class="fs-2 text-center my-5 mx-auto">
      Escribe tu opinion para el juego:
      <span class="fw-bold">{{ gameName }}</span>
    </h1>

    <b-form @submit="onSubmit" v-if="show" class="w-50 text-center mx-auto">
      <div class="mb-3">
        <b-form-input
          v-model="form.name"
          placeholder="Nombre completo"
          required
        ></b-form-input>
      </div>

      <div class="mb-3">
        <b-form-textarea
          v-model="form.opinion"
          placeholder="Escribe tu opinión..."
          rows="3"
          max-rows="6"
        ></b-form-textarea>
      </div>

      <b-button type="submit" variant="success" class="mt-4"
        >Agregar opinión</b-button
      >
    </b-form>

    <div class="">
      <h2 class="fs-2 text-center my-5 mx-auto">
        A continuación puedes ver tu opinión.
      </h2>
    </div>

    <!--opiniones-->
    <div
      v-if="opinions.length === 0"
      class="w-50 border border-secondary my-5 text-center mx-auto list-opinion bg-danger bg-opacity-50"
    >
      <p class="text-danger text-start ps-2 py-1">
        No existen opiniones par mostrar
      </p>
    </div>

    <div
      v-if="opinions.length > 0"
      class="w-50 border border-secondary my-5 text-center mx-auto list-opinion"
    >
      <ul class="w-100">
        <li v-for="opinion in opinions" :key="opinion.id">
          <div class="bg-info bg-opacity-50">
            <p class="text-primary text-start ps-2 py-2">
              Opinión creada por:
              <span class="fw-bold">{{ opinion.name }}</span>
            </p>
          </div>
          <div>
            <p class="text-start ps-2">
              <span class="fw-bold">Opinión: </span>{{ opinion.description }}
            </p>
            <div class="d-flex gap-2 mb-2 ms-2">
              <button
                @click="deleteGame(opinion.id)"
                class="btn btn-danger"
              >
                Eliminar
              </button>
              <button @click="editGame(opinion.id)" class="btn btn-warning">
                Editar
              </button>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
export default Vue.extend({
  name: "OpinionView",
  data() {
    return {
      form: {
        name: "",
        opinion: "",
      },
      show: true,
      opinions: [],
      gameName: "",
      idGame: null,
    };
  },
  methods: {
    deleteGame(id){
      // filtro enb las opiniones segun el id
      this.opinions = this.opinions.filter(opinion => opinion.id !== id);
      console.log(id)

      const allOpinions = JSON.parse(localStorage.getItem("opinions")) || {};
      const gameOpinions = allOpinions[this.idGame] || [];
        
      //eliminar la opinion
      const updateOpinion = gameOpinions.filter(opinion => opinion.id !== id);

      //actualizar localStorage
      allOpinions[this.idGame] = updateOpinion;
      localStorage.setItem("opinions", JSON.stringify(allOpinions));
      console.log("opinion id" + id + "eliminada");
        
      alert("Opinión eliminada");
    },
    editGame(id) {
      const newDescription = prompt('Actualiza tu opinión');
        
      const allOpinions = JSON.parse(localStorage.getItem("opinions")) || {};
      const gameOpinion = allOpinions[this.idGame] || [];
        
      //busacra opinion x id
      const editOpinion = gameOpinion.find(opinion => opinion.id === id);

      if(editOpinion) {
        editOpinion.description = newDescription;

        //guardar
        allOpinions[this.idGame] = gameOpinion;
        localStorage.setItem("opinions", JSON.stringify(allOpinions));

        //actualizar
        this.opinions = gameOpinion;
        console.log("Opinión con id " + id + " actualizada");
      }
    },
    onSubmit(event) {
      event.preventDefault();

      const newOpinion = {
        id: Date.now(),
        name: this.form.name,
        description: this.form.opinion,
        // Agregamos el id del juego para poder identificar de quien es el comentario
        idGame: this.idGame,
      };

      this.addOpinion(newOpinion);
      this.onReset();
    },
    addOpinion(opinion) {
      const allOpinions = JSON.parse(localStorage.getItem("opinions")) || {};

      if(!allOpinions[this.idGame]) {
        allOpinions[this.idGame] = [];
      }
      allOpinions[this.idGame].unshift(opinion);

      localStorage.setItem("opinions", JSON.stringify(allOpinions));
      this.opinions = allOpinions[this.idGame];
    },
      loadOpinions() {
        const allOpinions = JSON.parse(localStorage.getItem("opinions")) || {};
        this.opinions = allOpinions[this.idGame] || [];  
    },
    onReset() {
      this.form.name = "";
      this.form.opinion = "";
    },
  },
  created() {
    //Atraves de la url envio 2 valores como querys
    this.gameName = this.$route.query.name;
    this.idGame = this.$route.query.idGame;

    const infoOpinions = localStorage.getItem("opinions");

    if(infoOpinions) {
      let opinionGame = JSON.parse(infoOpinions);

    this.opinions = opinionGame[this.idGame] || [];
    }else {
      this.opinions = [];
    }
  },
});
</script>

<style>
  .list-opinion ul {
    list-style: none;
    margin: 0;
    padding: 0;
}
</style>