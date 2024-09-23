<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import HomeView from './views/HomeView.vue'
</script>

<template>
  <div class="app">
    <router-view></router-view>
  </div>
</template>

<style scoped>
  .app {
    height: 100%;
    width: 100%;
  }
</style>
