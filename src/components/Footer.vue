<script setup>
import { ref } from 'vue';
const text = ref('')
</script>
<template>
  <q-footer elevated class="secondary">
      <q-toolbar>
        <q-input
          dark
          standout="bg-primary text-white"
          label="Ingrese texto"
          v-model='text'
        ></q-input>
      </q-toolbar>
  </q-footer>
</template>
