<template>
  <router-view v-if="userGoogle!==false"/>
</template>

<script setup>
  import { provide, ref } from 'vue';
  import { getAuth, onAuthStateChanged } from 'firebase/auth';
  import { auth } from './firebase';
  import { useQuasar } from 'quasar';

  const userGoogle = ref(false)
  const $q = useQuasar()

  provide('userGoogle', userGoogle)
  onAuthStateChanged(auth, (user) => {
    userGoogle.value = user
    $q.loading.hide()
  })

  $q.loading.show({
  })
</script>
