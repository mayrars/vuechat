<script setup>
  import { inject } from 'vue';
  import {collection, query, onSnapshot, orderBy} from 'firebase/firestore'
  import { auth, db } from '../firebase';
  import { ref } from 'vue';

  const userGoogle = inject('userGoogle')
  const messages = ref([])

  const chatRef = ref(null)
  const q = query(collection(db, 'chats'), orderBy('time'))
  const unsubscribe = onSnapshot(q, (snapshot) => {
    snapshot.docChanges().forEach(async(change) => {
      if (change.type === 'added') {
        console.log('New chat: ', change.doc.data())
        messages.value.push({
          id: change.doc.id,
          ...change.doc.data()
        })
        await nextTick()
        window.scrollTo(0, document.body.scrollHeight)
      }
    })
  })
</script>
<template>
  <q-page v-if="!userGoogle">
    <h3 class="text-center text-primary">Inicia sesiòn</h3>
  </q-page>
  <q-page v-else padding>
    <div class="q-pa-md row justify-center" ref="chatRef">
      <div style="width: 100%; max-width: 400px">
        <template
          v-for="message in messages"
          :key="message.id"
        >
          <q-chat-message
            :text="[message.text]"
            :sent="message.uid=== auth.currentUser.uid"
            :name="message.displayName"
          />
        </template>
      </div>
    </div>
  </q-page>
</template>

