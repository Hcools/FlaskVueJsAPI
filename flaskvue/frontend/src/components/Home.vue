//Home.vue

<template>
  <div>
    <p>Home page</p>
    <p>Random number from backend: {{ randomNumber }}</p>
    <p>Un nom random: {{ nom }}</p>
    <button @click="getRandomFromBackend">New random number</button>
    <button @click="getNom">New random number</button>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      randomNumber: 0,
      nom: 'ola'
    }
  },
  methods: {
    getRandomInt (min, max) {
      min = Math.ceil(min)
      max = Math.floor(max)
      return Math.floor(Math.random() * (max - min + 1)) + min
    },
    getRandom () {
      this.randomNumber = this.getRandomInt(1, 100)
    },
   getRandomFromBackend () {
     console.log('appel');
     const path = `http://localhost:5000/api/random`
     axios.get(path)
     .then(response => {
       this.randomNumber = response.data.randomNumber
    })
    .catch(error => {
      console.log(error)
    })
   },
  getNom(){
    console.log('refffff'); 
     const path = `http://localhost:5000/api/random`
     axios.get(path)
     .then(response => {
	this.nom = response.data.nom
    })
    .catch(error => {
	console.log(error)
   })
  },
  created () {
    this.getRandom()
  }
}}
</script>
