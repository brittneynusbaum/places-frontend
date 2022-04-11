<script>import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      places: []
    };
  },
  created: function () {
    this.indexProducts()
  },
  methods: {
    indexProducts: function () {
      console.log('showing all products')
      axios.get('/places').then(response => {
        console.log(response.data)
        this.places = response.data
      });
    }
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="place in places" v-bind:key="place.id">
      <p>{{ place.name }}</p>
      </div>
</div>
</template>

<style>
</style>