<script>import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      places: [],
      newPlace: {}
    };
  },
  created: function () {
    this.indexPlaces()
  },
  methods: {
    indexPlaces: function () {
      console.log('showing all products')
      axios.get('/places').then(response => {
        console.log(response.data)
        this.places = response.data
      });
    },
    createPlace: function () {
      console.log('creating product')
      axios.post('/places', this.newPlace).then(response => {
        console.log(response.data)
        this.newPlace = {}
      });
    }
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h3>Create new place</h3>
    <p>Name: <input v-model="this.newPlace.name"></p>
    <p>Address: <input v-model="this.newPlace.address"></p>
    <button v-on:click="createPlace()">Save product</button>
    <hr>
    <h3>All places</h3>
    <div v-for="place in places" v-bind:key="place.id">
      <p>{{ place.name }}</p>
      </div>
</div>
</template>

<style>
</style>