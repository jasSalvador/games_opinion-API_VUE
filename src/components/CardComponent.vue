<template>
  <div>
    <b-card
      :title="gameProps.name"
      :img-src="gameProps.background_image"
      img-alt="Juego"
      img-top
      tag="article"
      style="max-width: 20rem"
      class="mb-2"
    >
      <b-card-text>
        <p class="border-bottom">Rating: {{ gameProps.rating }}</p>
        <p class="border-bottom">Released: {{ gameProps.released }}</p>
        <p class="border-bottom">Update: {{ gameProps.updated }}</p>
      </b-card-text>

      <div class="d-flex justify-content-star align-items-center gap-3">
        <b-button @click="nameGameOpinion" variant="primary">Opinar</b-button>

        <b-button
          @click="heartLike(gameProps.id, gameProps.name)"
          variant="secondary"
        >
          <i
            :id="'heart-icon-' + gameProps.id"
            :class="`bi bi-heart-fill px-1 ${
              heartRed[gameProps.id] || false ? 'text-danger' : 'text-light'
            }`"
          >
          </i>
        </b-button>
      </div>
    </b-card>
  </div>
</template>

<script>
import Vue from "vue";
export default Vue.extend({
  name: "cardComponent",
  data() {
    return {};
  },
  props: {
    gameProps: {
      type: Object,
      require: true,
    },
    heartRed: {
      type: Object,
    },
  },
  methods: {
    nameGameOpinion() {
      this.$router.push({
        name: "opinion",
        query: { name: this.gameProps.name, idGame: this.gameProps.id },
      });
    },
    heartLike(id, name) {
      this.$emit("heartClick", { id, name });
    },
  },
  mounted() {},
});
</script>

<style>
</style>