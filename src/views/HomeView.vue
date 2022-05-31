<script>
import axios from 'axios';
export default {
  data: function () {
    return {
      contacts: [],
      newContactParams: {}
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
      });
    },
    createContact: function() {
      axios
        .post("/contacts", this.newContactParams)
        .then((response) => {
          console.log("contact created", response);
          this.contacts.push(response.data);
          this.newContactParams = {};
        })
        .catch((error) => {
          console.log("contact creation error", error.response);
        });
    }
  },
};
</script>

<template>
  <div class="home">
    <h1>Contacts Page</h1>
    <div class="inputs">
      <div>
        First Name: 
        <input v-model="newContactParams.first_name" type="text">
      </div>
      <div>
        Last Name: 
        <input v-model="newContactParams.last_name" type="text">
      </div>
      <div>
        Email: 
        <input v-model="newContactParams.email" type="text">
      </div>
      <div>
        Phone Number: 
        <input v-model="newContactParams.phone_number" type="text">
      </div>
      <div>
        Image: 
        <input v-model="newContactParams.image" type="text">
      </div>
    </div>


    <h3>Add / Update / Destroy Contact</h3>
    <div class="button">
      <button v-on:click="createContact()">Create Contact</button>
    </div>
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