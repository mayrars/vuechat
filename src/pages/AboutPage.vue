<template>
  <q-page padding>
    <h1>About</h1>
  <div class="q-pa-md row justify-center">
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
  </div>
  </q-page>
</template>
