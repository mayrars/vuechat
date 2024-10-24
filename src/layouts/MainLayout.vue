<template>
  <q-layout view="hHr lpR fFr">
    <Navbar />
    <q-page-container>
      <router-view />
    </q-page-container>
    <Footer />
  </q-layout>
</template>

<script setup>
import Navbar from 'src/components/Navbar.vue';
import Footer from 'src/components/Footer.vue';
</script>
