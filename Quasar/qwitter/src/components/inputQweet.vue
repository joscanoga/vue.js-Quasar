<script setup>
import { ref } from 'vue'
import { collection, addDoc } from '@firebase/firestore';
import {auth, db} from "../firebase"
const newQueetContent = ref('')
const addQweet = () => {
  if(newQueetContent.value.trim() != ''){
    addDoc(collection(db,'Qweets'),{
    QweetContent: newQueetContent.value,
    uid: auth.currentUser.uid,
    time: Date.now()  ,
    displayName: auth.currentUser.displayName
  })
  .then(()=>{
    newQueetContent.value = '';
    console.log("aqui iria un sonido")
  })
  .catch((error) => {
    console.error("Error adding document: ", error);
  });
  }else{
    alert("No puedes enviar un Qweet vacio")
    text.value = '';
  }

}


</script>

<template>
  <div class="q-py-lg q-px-md row items-end q-col-gutter-md">
      <div class="col  ">
        <q-input class="newQuweet" bottom-slots v-model="newQueetContent" placeholder="What's happening?" counter
          maxlength="250" autogrow @keyup.enter="addQweet" dense>
          <template v-slot:before>
            <q-avatar size="xl">
              <img src="https://cdn.quasar.dev/img/avatar5.jpg">
            </q-avatar>
          </template>
        </q-input>
      </div>
      <div class="col col-shrink">

        <q-btn @click="addQweet" unelevated rounded color="primary" label="Qweet" no-caps :disable="!newQueetContent && true" />

      </div>
    </div>
</template>


<style scoped>

</style>
