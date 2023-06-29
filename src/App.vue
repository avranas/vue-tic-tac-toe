<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
import BoardComponent from './components/BoardComponent.vue'
</script>

<template>
  <header><h1>Vue Tic Tac Toe</h1></header>

  <!-- Put your board here -->
  <BoardComponent />
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
}

  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

</style>
