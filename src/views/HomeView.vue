<template>
  <div class="container">
    <h1>Bienvenue sur Vera Virtual</h1>

    <p>
      cliquez
      <a href="http://localhost:8080/api/restaurants/create">ici</a> pour
      ajouter votre restaurant
    </p>
  </div>
</template>

<script>
// @ is an alias to /src
import RestaurantCreate from "@/components/RestaurantCreate.vue";

export default {
  name: "HomeView",
  components: {
    RestaurantCreate,
  },
};
</script>
<style>
.container {
  margin-top: 10vh;
}
</style>
