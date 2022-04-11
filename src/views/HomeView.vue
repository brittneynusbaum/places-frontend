<script>import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      places: [],
      newPlace: {},
      currentPlace: {}
    };
  },
  created: function () {
    this.indexPlaces()
  },
  methods: {
    indexPlaces: function () {
      console.log('showing all places')
      axios.get('/places').then(response => {
        console.log(response.data)
        this.places = response.data
      });
    },
    createPlace: function () {
      console.log('creating place')
      axios.post('/places', this.newPlace).then(response => {
        console.log(response.data)
        this.newPlace = {}
      });
    },
    showPlace: function (place) {
      console.log('show place')
      this.currentPlace = place
      document.querySelector("#fruit-details").showModal();

    }
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <hr>
    <h3>Create new place</h3>
    <p>Name: <input v-model="this.newPlace.name"></p>
    <p>Address: <input v-model="this.newPlace.address"></p>
    <button v-on:click="createPlace()">Save product</button>
    <hr>
    <h3>All places</h3>
    <div v-for="place in places" v-bind:key="place.id">
      <p>{{ place.name }}</p>
      <button v-on:click="showPlace(place)">More info</button>
    </div>
    <dialog id="fruit-details">
      <form method="dialog">
        <h3>Place info</h3>
        <p>Name: {{ currentPlace.name }}</p>
        <p>Address: {{ currentPlace.address }}</p>
        <button>Close</button>
      </form>
      </dialog>
</div>
</template>

<style>
</style>