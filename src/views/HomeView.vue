<script>
import axios from 'axios';
export default {
  data: function () {
    return {
      contacts: []
    };
  },
  created: function () {
    this.indexContacts();
  },
  methods: {
    indexContacts: function() {
      axios.get("/contacts").then((response) => {
        console.log("contacts index", response);
        this.contacts = response.data;
      })
    }
  },
};
</script>

<template>
  <div class="home">
    <h1>Contacts</h1>
    <div v-for="contact in contacts" v-bind:key="contact.id">
      <div class="image">
        <img v-bind:src="contact.image" v-bind:alt="contact.name">       
      </div>
      <h2>{{ contact.first_name }} {{ contact.last_name }}</h2>
      <h3>{{contact.email}} * {{contact.phone_number}}</h3>
    </div>
  </div>
</template>

<style>
  img {
      max-width: 50%;
  }
</style>