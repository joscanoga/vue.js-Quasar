<script setup>
import { ref } from 'vue'
import { collection, addDoc } from '@firebase/firestore';
import {auth, db} from "../firebase"
const text = ref('')
const addText = () => {
  addDoc(collection(db,'chats'),{
    text: text.value,
    uid: auth.currentUser.uid,
    time: Date.now()  ,
    displayName: auth.currentUser.displayName
  })
  .then(()=>{
    text.value = '';
    console.log("aqui iria un sonido")
  })
  .catch((error) => {
    console.error("Error adding document: ", error);
  });
}
</script>

<template>
  <q-input dense class="full-width" outlined bottom-slots v-model="text" label="Mensaje"  @keyup="addText" >

    <template v-slot:append>
      <q-btn round dense flat icon="send" class="cusor-pointer " type="submit" @click="addText"/>
    </template>
  </q-input>
</template>


<style scoped></style>
