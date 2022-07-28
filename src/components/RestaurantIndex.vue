<template>
  <h2>Liste des restaurants</h2>

  <p>
    <span>Nom</span> <span>Adresse</span> <span>Horaires d'ouverture</span>
    <span>Horaires de fermeture</span>
  </p>

  <p v-for="item in list" :key="item">
    <span>{{ item.name }}</span> <span>{{ item.adresse }}</span>
    <span>{{ item.horaires }}</span> <span>{{ item.closed }}</span>
    <button @click="show(item.id)">Modifier</button>
    <button @click="delete1(item.id)">Delete</button>
  </p>

  <h2 v-if="name != ''">Modifier un restaurant</h2>

  <form @submit="modifier(id)" v-if="name != ''">
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
</template>

<script>
import RestaurantEdit from "@/components/RestaurantEdit.vue";
export default {
  components: {
    RestaurantEdit,
  },
  data() {
    return {
      list: [],
      id: "",
      name: "",
      adresse: "",
      horaires: "",
      closed: "",
    };
  },

  methods: {
    async delete1(id) {
      const options = {
        method: "delete",
        headers: {
          "Content-Type": "application/json ",
          Accept: "application/json ",
        },
      };

      const response = await fetch(
        "http://127.0.0.1:8000/api/restaurants/" + id,
        options
      );

      const data = await response.json();
      console.log(data);

      window.location.reload();
    },
    async afficher() {
      const options = {
        method: "GET",
        headers: {
          "Content-Type": "application/json ",
          Accept: "application/json ",
        },
      };

      const response = await fetch(
        "http://127.0.0.1:8000/api/restaurants",
        options
      );

      const data = await response.json();
      this.list = data.restaurant;

      console.log(data);
    },

    async show(id) {
      const options = {
        method: "GET",
        headers: {
          "Content-Type": "application/json ",
          Accept: "application/json ",
        },
      };

      const response = await fetch(
        "http://127.0.0.1:8000/api/restaurants/" + id,
        options
      );

      const data = await response.json();
      this.id = data.restaurant.id;
      this.name = data.restaurant.name;
      this.adresse = data.restaurant.adresse;
      this.horaires = data.restaurant.horaires;
      this.closed = data.restaurant.closed;

      console.log(data);

      /* this.$router.push("edit");
      console.log("hello"); */

      /* window.location.href =
        "http://127.0.0.1:8000/api/restaurants/" + id + "/edit"; */
    },
    async modifier(id) {
      const options = {
        method: "PUT",
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
      console.log("data.restaurant");
    },
  },

  mounted() {
    this.afficher();
  },
};
</script>

<style>
p {
  display: flex;
  justify-content: space-around;
}
</style>
