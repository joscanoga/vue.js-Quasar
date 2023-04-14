<script setup>
import { inject, ref } from 'vue'
import { GoogleAuthProvider, signInWithPopup, signOut } from "firebase/auth";
import { auth } from '../firebase';

const leftDrawerOpen = inject('leftDrawerOpen')
const rightDrawerOpen = inject('rightDrawerOpen')
const userGoogle = inject('userGoogle')



const toggleLeftDrawer= () =>{
      leftDrawerOpen.value = !leftDrawerOpen.value
    }


const toggleRightDrawer =() =>{
      rightDrawerOpen.value = !rightDrawerOpen.value
    }
const loginGoogle = () => {
  console.log('login google')
  const provider = new GoogleAuthProvider();
  signInWithPopup(auth,provider).catch(e=>console.log(e))

}
const logoutGoogle = () => {
  signOut(auth).catch((error) => {
    console.log(error)
  });
}

</script>
<template>
  <q-header elevated class="bg-primary text-white" height-hint="98">
    <q-toolbar>
      <q-btn dense flat round icon="menu" @click="toggleLeftDrawer" v-show="userGoogle"/>

      <q-toolbar-title>
        <q-avatar>
          <img src="https://cdn.quasar.dev/logo-v2/svg/logo-mono-white.svg">
        </q-avatar>
        Quasar Chat
      </q-toolbar-title>
      <q-btn label="Ingresar" color="secondary" @click="loginGoogle" v-show="!userGoogle"></q-btn>
      <q-btn label="Salir" color="accent" @click="logoutGoogle" v-show="userGoogle"></q-btn>
      <q-btn dense flat round icon="menu" @click="toggleRightDrawer" v-show="userGoogle"/>
    </q-toolbar>

    <q-tabs align="left">
      <q-route-tab to="/" label="Home" />
      <q-route-tab to="/chat" label="chat" v-if="userGoogle"/>
      <q-route-tab to="/about" label="about" />
    </q-tabs>
  </q-header>



</template>
<style scoped></style>
