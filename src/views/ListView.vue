<script setup>
import { ref } from 'vue';
import axios from 'axios';
import { RouterLink } from 'vue-router'


let amiibos = ref()


axios.get("https://amiiboapi.com/api/amiibo/").then((response) => {
  amiibos.value = response.data.amiibo
}).catch((error) => {
  console.log(error);
})


</script>

<template>

  <section id="main">
    <div class="container">
      <article class="box post">
        <header>
          <h2>Ma Collection</h2>
        </header>
        <p>
        <table>
          <tr>
            <th>Character</th>
            <th>game Series</th>
            <th>Action</th>
          </tr>
          <tr v-for="amiibo in amiibos" :key="amiibo.tail">
            <td>{{ amiibo.name }}</td>
            <td>{{ amiibo.gameSeries }}</td>
            <td><RouterLink :to="'/amiiboDetail/' + amiibo.tail"><button>Voir</button></RouterLink></td>
          </tr>
        </table>
        </p>
      </article>
    </div>
  </section>
</template>

<style>


</style>
