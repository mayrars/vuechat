<script setup>
import { ref, inject } from 'vue'
import { GoogleAuthProvider, signInWithPopup, signOut } from 'firebase/auth';
import { auth, db } from '../firebase';
import InfoUser from './InfoUser.vue';

const rightDrawerOpen = ref(false)
const userGoogle = inject('userGoogle')

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
      <q-btn label="Ingresar" color="secondary" @click="accessGoogle" v-if="!userGoogle"></q-btn>
      <q-btn label="Salir" color="secondary" @click="logoutGoogle" v-if="userGoogle"></q-btn>
      <q-btn dense flat round icon="menu" @click="toggleRightDrawer" v-if="userGoogle"/>
    </q-toolbar>
  </q-header>

  <q-drawer v-model="rightDrawerOpen" side="right" behavior="mobile" bordered v-if="userGoogle">
    <info-user />
  </q-drawer>
</template>
