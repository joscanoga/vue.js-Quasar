<script setup>
import InputChat from 'src/components/InputChat.vue'
import { inject, ref, nextTick, watchEffect } from 'vue'
import { collection, query, onSnapshot, orderBy,limit } from "firebase/firestore";
import { db } from "../firebase"
const userGoogle = inject('userGoogle')
const menssages = ref([])
const chatRef = ref(null);
let reverse = true;
//watchEffect es un metodo similar a un useEffect de react js
watchEffect(async ( onCleanup ) =>{

  if (userGoogle.value) {
    const q = query(collection(db, "chats"), orderBy("time","desc"),limit(15));
    const unsubscribe = onSnapshot(q, (snapshot) => {
      snapshot.docChanges().forEach(async (change) => {
        
        if (change.type === "added") {

          menssages.value.push({
            id: change.doc.id,
            //trae los datos del documento y los guarda en el objeto actual
            ...change.doc.data()
          });

          //baja el scroll al ultimo mensaje
          await nextTick();
          chatRef.value.scrollTop = chatRef.value.scrollHeight;
        }

      });
      if(reverse){
      menssages.value=menssages.value.reverse();
      reverse = false;
    }
    });


    onCleanup(unsubscribe)

  }

})

</script>
<template>
  <body>
    <q-page class="alert" v-if="!userGoogle">
      <h3 class="bg-warning text-center text-red-14">Debes iniciar sesión</h3>
    </q-page>
    <q-page v-else padding class="container-chat" >
      <div class="q-pa-md row justify-center mensajes "  ref="chatRef">

        <div style="width: 100%; max-width: 1000px ;height: auto;" >
          <template v-for="mensage in menssages" :key="mensage.id">
            <q-chat-message :name="mensage.displayName" :text="[mensage.text]" :sent="mensage.uid === userGoogle.uid" />
            <br>
          </template>

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

.input {
  position: absolute;
  bottom: 0;
  width: 95%;
  height: 10%;

  justify-content: center;

}

.mensajes {
  height: 90%;
  overflow-y: scroll;

}
.container-chat {
  height: 700px;
	border: 1px solid #ddd;
	background: #f1f1f1;


}
</style>
