<script setup>
  import { inject } from 'vue';

  const userGoogle = inject("userGoogle")
</script>
<template>
  <q-page v-if="!userGoogle">
    <h3 class="text-center text-primary">Inicia sesiòn</h3>
  </q-page>
  <q-page v-else padding>
    <div style="width: 100%; max-width: 400px">
      <q-chat-message
        :text="['hey, how are you?']"
        sent
        name="me"
      />
      <q-chat-message
        :text="['doing fine, how r you?']"
        name="Luis"
      />
    </div>
  </q-page>
</template>

