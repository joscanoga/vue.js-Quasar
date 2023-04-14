<script setup>
import InputChat from 'src/components/InputChat.vue'
import { inject } from 'vue'
const userGoogle = inject('userGoogle')
</script>
<template>
  <body>
    <q-page class="alert" v-if="!userGoogle">
      <h3 class="bg-warning ">Debes iniciar sesión</h3>
    </q-page>
    <q-page v-else padding>
      <div class="q-pa-md row justify-center mensajes">
        <div style="width: 100%; max-width: 1000px">
          <q-chat-message name="me" :text="['hey, how are you?']" sent />
          <q-chat-message name="Jane" :text="['doing fine, how r you?']" />
        </div>
      </div>
      <div class="input">
        <InputChat />
      </div>
    </q-page>
  </body>
</template>

<style scoped>
.alert {
  padding: 1rem;
  text-align: center;
  justify-content: center;
}

.input{
  position: absolute;
  bottom: 0;
  width: 95%;
  height: 10%;

  justify-content: center;

}
.mensajes{
  max-height: 90%;
}
</style>
