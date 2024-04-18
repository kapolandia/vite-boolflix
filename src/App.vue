<script setup>
import AppHeader from './components/AppHeader.vue'
import AppCards from './components/AppCards.vue'

</script>

<template>
  <body>
    <header>
      <AppHeader></AppHeader>
    </header>

    <main>
      <AppCards></AppCards>
    </main>
  </body>
</template>

<style >
  body{
    background-color: #1C1C1C;
    overflow-x: hidden;
  }
</style>
