<template>
  <router-view v-if="userGoogle !== false" />
</template>

<script setup>
import {  onAuthStateChanged } from "firebase/auth";
import { auth } from "./firebase";
import { provide, ref } from 'vue'
import { useQuasar } from 'quasar'
const userGoogle = ref(false)
const $q = useQuasar()
const leftDrawerOpen = ref(false)
provide('leftDrawerOpen', leftDrawerOpen)
const rightDrawerOpen = ref(false)
provide('rightDrawerOpen', rightDrawerOpen)

provide('userGoogle', userGoogle)
//metodo para saber si hay un usuario logueado y hacerle seguimiento
onAuthStateChanged(auth, (user) => {

    // User is signed in, see docs for a list of available properties
    // https://firebase.google.com/docs/reference/js/firebase.User
  userGoogle.value = user;
  setTimeout(() => {
    $q.loading.hide()
  }, 400);
    // ...


});


$q.loading.show()
</script>
