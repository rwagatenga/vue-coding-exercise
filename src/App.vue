<template>
  <div id="app" class="md:container md:mx-auto p-5">
    <app-card></app-card>
  </div>
</template>

<script>
import Card from "./components/card/Card.vue";
export default {
  components: { "app-card": Card },
};
</script>

<style scoped>
div .card-body {
  background-color: #012672;
}
</style>
