<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      fruits: []
    };
  },
  created: function () {
    console.log("in create");
    this.indexFruits();
  },
  methods: {
    indexFruits: function () {
      console.log("index fruits");
      axios.get("/fruits.json").then(response => {
        console.log(response.data);
        console.log(response)
        this.fruits = response.data;
      });
    }
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for:="fruit in fruits" v-bind:key="fruit.id">
      <h3>{{ fruit.name }}</h3>
      <img v-bind:src="fruit.image" v-bind:alt="fruit.name" />
      <p>kind: {{ fruit.kind }}</p>
      <p>quantity: {{ fruit.quantity }}</p>
    </div>
    <button v-on:click="indexFruits()">index fruits</button>
  </div>
</template>

<style>
img {
  width: 150px;
}
</style>