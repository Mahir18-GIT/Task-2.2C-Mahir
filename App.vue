<template>
  <div id="app">
    <header>
      <h1>Virtual Museum Explorer</h1>
    </header>
    <MuseumExplorer></MuseumExplorer>
  </div>
</template>

<script>
import MuseumExplorer from './components/MuseumExplorer.vue';

export default {
  name: 'App',
  components: {
    MuseumExplorer
  }
}
</script>

<style>
/* You can add global styles or reset/normalize styles here */
</style>
