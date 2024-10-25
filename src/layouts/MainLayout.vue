<template>
  <q-layout view="hHr lpR fFr">
    <navbar />
    <q-page-container>
      <router-view />
    </q-page-container>
    <footer />
  </q-layout>
</template>

<script setup>
import {inject} from 'vue'
import Navbar from 'src/components/Navbar.vue';
import Footer from 'src/components/Footer.vue';

const userGoogle = inject("userGoogle")

</script>
