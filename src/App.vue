<template>
  <div id="app">
    <h1>Воркшоп: Работа с формами (Домашняя работа)</h1>
    <Form
      :citizenships="preparedCitizen"
      :passportTypes="preparedPassportTypes"
    />
  </div>
</template>

<script>
import Form from "./components/Form.vue";
import citizenships from "./assets/data/citizenships.json";
import passportTypes from "./assets/data/passport-types.json";

export default {
  name: "App",
  components: {
    Form,
  },
  data() {
    return {
      citizenships,
      passportTypes,
    };
  },
  computed: {
    preparedCitizen() {
      return this.citizenships.map((item) => ({
        id: item.id,
        name: item.nationality,
      }));
    },
    preparedPassportTypes() {
      return this.passportTypes.map((item) => ({
        id: item.id,
        name: item.type,
      }));
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  background-color: #f9f9fd;
  padding: 24px;
  box-sizing: border-box;
}

html,
body {
  margin: 0;
  height: 100vh;
}

#app {
  min-height: 100vh;
}

* {
  box-sizing: border-box;
}
</style>
