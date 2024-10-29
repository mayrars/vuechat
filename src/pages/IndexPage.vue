<script setup>
  import { inject } from 'vue';
  import {collection, query, onSnapshot, orderBy} from 'firebase/firestore'
  import { auth, db } from '../firebase';
  import { ref } from 'vue';

  const userGoogle = inject('userGoogle')
  const messages = ref([])

  const chatRef = ref(null)
  const q = query(collection(db, 'chats'), orderBy('time'))
  const unsubscribe = onSnapshot(q, async(snapshot) => {
    snapshot.docChanges().forEach((change) => {
      if (change.type === 'added') {
        messages.value.push({
          id: change.doc.id,
          ...change.doc.data()
        })
      }
    });
    await nextTick()
    chatRef.value.scrollTo(0, chatRef.value.scrollHeight)
  })
</script>
<template>
  <q-page v-if="!userGoogle">
    <h3 class="text-center text-primary">Inicia sesiòn</h3>
  </q-page>
  <q-page v-else padding>
    <div class="q-pa-md row justify-center scrollChat" ref="chatRef">
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

<style>
.scrollChat{
  height: calc(100vh - 100px);
  overflow-y: scroll;
}
</style>
