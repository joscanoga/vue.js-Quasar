<script setup>
import { inject } from 'vue';
import { GoogleAuthProvider, signInWithPopup, signOut } from "firebase/auth";
import { auth } from '../firebase';
const leftDrawerOpen = inject('leftDrawerOpen')
const rightDrawerOpen = inject('rightDrawerOpen')
const userGoogle = inject('userGoogle')



const toggleLeftDrawer = () => {
  leftDrawerOpen.value = !leftDrawerOpen.value
}

const toggleRightDrawer = () => {
  rightDrawerOpen.value = !rightDrawerOpen.value
}
const loginGoogle = () => {
  console.log('login google')
  const provider = new GoogleAuthProvider();
  signInWithPopup(auth, provider).catch(e => console.log(e))

}
const logoutGoogle = () => {
  signOut(auth).catch((error) => {
    console.log(error)
  });
}
</script>

<template>
  <q-header bordered class="bg-white text-black text-center">
    <q-toolbar>
      <q-btn dense flat round icon="menu" @click="toggleLeftDrawer" />


      <q-toolbar-title class="text-weight-bold ">
        <span class="gt-sm">Qwitter</span>
        <q-icon name="mdi-bird" class=" text-primary q-pa-md lt-md absolute-center" size="sm" />
      </q-toolbar-title>
      <q-btn label="Ingresar" color="secondary" @click="loginGoogle" v-show="!userGoogle"></q-btn>
      <q-btn label="Salir" color="accent" @click="logoutGoogle" v-show="userGoogle"></q-btn>
      <q-btn dense flat round icon="menu" @click="toggleRightDrawer" />


    </q-toolbar>
  </q-header>
</template>


<style scoped></style>
