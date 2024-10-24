<template>
  <router-view />
</template>

<script setup>
  import { getAuth, onAuthStateChanged } from 'firebase/auth';
  import { auth } from './firebase';
  onAuthStateChanged(auth, (user) => {
    if(user){
      const uid = user.uid;
    }else{

    }
  })
  if(user)
</script>
