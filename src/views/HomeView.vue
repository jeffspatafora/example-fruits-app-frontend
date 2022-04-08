<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      fruits: [],
      newFruitParams: {
        kind: "",
        name: "",
        quantity: "",
        image: ""
      },
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
        console.log(response);
        this.fruits = response.data;
      });
    },
    createFruit: function () {
      console.log("create fruits");
      axios.post("/fruits.json", this.newFruitParams).then(response => {
        console.log(response.data);
        this.fruits.push(response.data);
        this.newFruitsParams = {};
      });
    }
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <p>
      kind
      <input type="text" v-model="newFruitParams.kind" />
    </p>
    <p>
      name
      <input type="text" v-model="newFruitParams.name" />
    </p>
    <p>
      quantity
      <input type="text" v-model="newFruitParams.quantity" />
    </p>
    <p>
      image
      <input type="text" v-model="newFruitParams.image" />
    </p>
    <button v-on:click="createFruit()">add a fruit</button>
    <div v-for:="fruit in fruits" v-bind:key="fruit.id">
      <h3>{{ fruit.name }}</h3>
      <img v-bind:src="fruit.image" v-bind:alt="fruit.name" />
      <p>kind: {{ fruit.kind }}</p>
      <p>quantity: {{ fruit.quantity }}</p>
      <hr />
    </div>
    <button v-on:click="indexFruits()">index fruits</button>
  </div>
</template>

<style>
img {
  width: 150px;
}
</style>