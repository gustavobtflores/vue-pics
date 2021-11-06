<template>
  <h1>{{ title }}</h1>
  <button v-on:click="moreCats">Mais gatinhos</button>
  <div v-if="loading">
    <p>Carregando...</p>
  </div>
  <ul v-else>
    <li class="card" v-for="(cat, index) in cats" :key="index">
      <img
        style="width: 300px; height: 300px; object-fit: cover"
        :src="cat.url"
      />
      <p>{{ facts[index].fact }}</p>
    </li>
  </ul>
</template>
<script>
import axios from "axios";

export default {
  data() {
    return {
      title: "Cats pics",
      loading: true,
      cats: [],
      facts: [],
    };
  },

  created() {
    this.catsPhotos();
    this.getCatsFacts();
  },

  methods: {
    async catsPhotos() {
      this.loading = true;
      await axios
        .get("https://api.thecatapi.com/v1/images/search?limit=12", {
          headers: {
            "x-api-key": "082cbc55-c552-4333-86b7-c84f16ddaa7f",
          },
        })
        .then((response) => {
          var photos = response.data;
          this.cats = photos;
          this.loading = false;
        })
        .catch((error) => {
          console.log(error);
        });
    },

    async getCatsFacts() {
      await axios
        .get("https://catfact.ninja/facts?limit=12")
        .then((response) => {
          var facts = response.data.data;
          this.facts = facts;
          console.log(facts[0].fact);
        })
        .catch((e) => {
          console.log(e);
        });
    },

    moreCats() {
      this.catsPhotos();
      this.getCatsFacts();
    },
  },
};
</script>
<style lang="scss">
@import "../../assets/scss/reset.scss";
@import "./style.scss";
</style>
