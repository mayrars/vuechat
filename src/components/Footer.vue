<script setup>
import { ref } from 'vue';
import { collection, addDoc } from 'firebase/firestore';
import { db, auth } from '../firebase';

const text = ref('')
const addText=()=>{
  addDoc(collection(db, 'chats'),{
    text: text.value,
    uid: auth.currentUser.uid,
    time: Date.now(),
    displayName: auth.currentUser.displayName
  })
  .catch(e=>{
    console.log(e)
  })
}
</script>
<template>
  <q-footer elevated class="secondary">
      <q-toolbar>
        <q-input
          class="full-width"
          dark
          dense
          standout
          label="Ingrese texto"
          v-model='text'
        >
          <template #append>
            <q-icon name="send" class="cursor-pointer" @click="addText"/>
          </template>
        </q-input>
      </q-toolbar>
  </q-footer>
</template>
