<template>
  <PhotosList />
</template>

<script>
import PhotosList from "./components/PhotosList";

export default {
  name: "App",
  components: {
    PhotosList,
  },
};
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1 {
  font-size: 2rem;
  font-weight: 400;
  margin-bottom: 2.5rem;
}
</style>
