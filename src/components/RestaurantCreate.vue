<template>
  <form @submit.prevent="ajouter">
    <h2>Ajoutez votre restaurant</h2>
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
    async ajouter() {
      const options = {
        method: "POST",
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
        "http://127.0.0.1:8000/api/restaurants",
        options
      );

      const data = await response.json();
      console.log(data);
    },
  },
};
</script>

<style>
form {
  border: solid 2px gray;
  margin-top: 5%;
  margin-left: auto;
  margin-right: auto;
  width: 25vw;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  border-radius: 10px;
}

input {
  margin: 10px;
}
label {
  margin: 10px;
}
</style>
