<template>
  <form @submit.prevent="modifier">
    <label for="">Nom du restaurant</label>
    <input type="text" name="name" id="name" v-model="name" />
    <label for="">Adresse du restaurant</label>
    <input type="text" name="adresse" id="adresse" v-model="adresse" />
    <label for="">Horaires d'ouverture du restaurant</label>
    <input type="time" name="horaires" id="horaires" v-model="horaires" />
    <label for="closed">Horaires de fermeture du restaurant</label>
    <input type="time" name="closed" id="closed" v-model="closed" />
    <input type="submit" value="Valider" />
  </form>

  <p>{{ id }}</p>
</template>

<script>
export default {
  data() {
    return {
      name: "",
      adresse: "",
      horaires: "",
      closed: "",
    };
  },

  methods: {
    async modifier(id) {
      const options = {
        method: "put",
        headers: {
          "Content-Type": "application/json ",
          Accept: "application/json ",
        },
        body: JSON.stringify({
          name: this.name,
          adresse: this.adresse,
          horaires: this.horaires,
          closed: this.closed,
        }),
      };

      const response = await fetch(
        "http://127.0.0.1:8000/api/restaurants/" + id,
        options
      );

      const data = await response.json();
      console.log(data.restaurant.id);
    },

    async afficher() {
      const options = {
        method: "GET",
        headers: {
          "Content-Type": "application/json ",
          Accept: "application/json ",
        },
      };

      const response = fetch(
        "http://127.0.0.1:8000/api/restaurants/{id}",
        options
      );

      const data = await response.json();
      this.id = data.restaurant.id;

      console.log(data.restaurant.id);
    },

    mounted() {
      this.afficher();
    },
  },
};
</script>

<style></style>
