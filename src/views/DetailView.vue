<script setup>

import axios from 'axios';
import { ref } from 'vue';
import { useRoute } from 'vue-router';

let amiibo = ref({})
const route = useRoute();


axios.get("https://amiiboapi.com/api/amiibo/?tail=" + route.params.tail).then((response) => {
  amiibo.value = response.data.amiibo[0]
}).catch((error) => {
  console.log(error);
})



</script>

<template>
  <section id="main">
    <div class="container">
      <div class="row">
        <div v-if="amiibo != null" class="col-4 col-12-medium">
          <section class="box">
            <header>
              <h3>Infos</h3>
            </header>
            <p> amiiboSeries: <b>{{amiibo.amiiboSeries}}</b> <br />
              character: {{amiibo.character}}<br />
              gameSeries: {{amiibo.gameSeries}}<br />
              type: {{amiibo.type}}
            </p>
          </section>
          <section class="box">
            <header>
              <h3>Dates sorties</h3>
            </header>
            <ul v-if="amiibo.release != undefined" class="divided">
              <li>au: {{amiibo.release.au ?? "Aucune date de sortie"}}</li>
              <li>eu: {{amiibo.release.eu ?? "Aucune date de sortie"}}</li>
              <li>jp : {{amiibo.release.jp ?? "Aucune date de sortie"}}</li>
              <li>na : {{amiibo.release.na ?? "Aucune date de sortie"}}</li>
            </ul>
          </section>
        </div>
        <div class="col-8 col-12-medium imp-medium">
          <article class="box post">
            <a href="#" class="featured"><img
                :src="amiibo.image"
                alt="" /></a>
            <header>
              <h2>{{amiibo.name}}</h2>
              <p>{{amiibo.type}}</p>
            </header>
          </article>
        </div>
      </div>
    </div>
  </section>
</template>

<style>


</style>
