<script setup>

import { ref } from 'vue';
import { RouterLink, useRoute } from 'vue-router'
import axios from 'axios';

let amiibos = ref()
const myAmiibosId = ["00350102","00380102","00360102"]
let myAmiibos = ref([])


myAmiibosId.forEach(element => {
  axios.get("https://amiiboapi.com/api/amiibo/?tail=" + element).then((response) => {
    myAmiibos.value.push(response.data.amiibo[0])
    console.log(response.data.amiibo[0]);
  }).catch((error) => {
    console.log(error);
  })
});


</script>

<template>
  <!-- Banner -->
    <section id="banner">
      <header>
        <h2>Hey.Bienvenue sur ma collection</h2>
      </header>
    </section>

  <!-- Intro -->
    <section id="intro" class="container">
      <div class="row">
        <div class="col-4 col-12-medium" v-for="amiido in myAmiibos" :key="amiido.tail">
          <section class="middle">
            <img :src="amiido.image" />
            <h2>{{amiido.character}}</h2>
            <p>{{amiido.gameSeries}}</p>
          </section>
        </div>
        
      </div>
      <footer>
        <ul class="actions">
          <li><RouterLink class="button large" :to="{ name: 'list' }">Liste complète</RouterLink></li>
        </ul>
      </footer>
    </section>

</template>
