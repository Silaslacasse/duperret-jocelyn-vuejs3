<script setup>
import { RouterLink, useRoute } from 'vue-router'
import { ref, watch } from 'vue';

const route = useRoute();
const currentRoute = ref(route.name);

watch(() => route, () => {
  currentRoute.value = route.name;
}, { deep: true })

</script>

<template>
  <section id="header">  
    <h1><a href="index.html">AmiiVue</a></h1>

    <nav id="nav">
      <ul>
        <li :class="{ 'current': currentRoute === 'home' }" > 
          <RouterLink :to="{ name: 'home' }">Home</RouterLink>
        </li>
        <li :class="{ 'current': currentRoute === 'list' }"> <RouterLink :to="{ name: 'list' }">Liste Amiibo</RouterLink></li>
      </ul>
    </nav>
  </section>
</template>

<style scoped>
</style>
