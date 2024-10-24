<script setup>
import { ref } from 'vue'
import { GoogleAuthProvider, signInWithPopup, signOut } from 'firebase/auth';
import { auth, db } from '../firebase';
const rightDrawerOpen = ref(false)

const toggleRightDrawer = () => {
  rightDrawerOpen.value = !rightDrawerOpen.value
}

const accessGoogle = () => {
  const provider = new GoogleAuthProvider();
  signInWithPopup(auth, provider).catch(error=> console.log(error))
}
const logoutGoogle = () => {
  signOut(auth).catch(error=> console.log(error))
}
</script>
<template>
  <q-header elevated class="bg-primary text-white">
    <q-toolbar>
      <q-toolbar-title>
        Chat
      </q-toolbar-title>
      <q-btn label="Ingresar" color="secondary" @click="accessGoogle"></q-btn>
      <q-btn label="Salir" color="secondary" @click="logoutGoogle"></q-btn>
      <q-btn dense flat round icon="menu" @click="toggleRightDrawer" />
    </q-toolbar>
  </q-header>

  <q-drawer v-model="rightDrawerOpen" side="right" behavior="mobile" bordered>
    <!-- drawer content -->
  </q-drawer>
</template>
