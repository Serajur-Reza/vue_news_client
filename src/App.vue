<template>
  <div class="container text-center" id="app">
    <h1 class="text-center">News Client</h1>
    <News />
  </div>
</template>

<script>
import News from "./components/News";

export default {
  name: "App",
  components: {
    News,
  },
};
</script>

<style>
</style>