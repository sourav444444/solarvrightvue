<template>
  <div class="bg-slate-50 min-h-screen text-slate-800">
    <Navbar />
    <router-view />
  </div>
</template>

<script setup>
import Navbar from './components/Navbar.vue'
</script>
