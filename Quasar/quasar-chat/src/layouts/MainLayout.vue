<template>
  <q-layout view="hHh lpR fFf">
    <Navbar />
    <Drawerleft v-show="userGoogle"/>
    <DrawerRight v-show="userGoogle"/>




    <q-page-container>
      <router-view />
    </q-page-container>

    <footer-add/>

  </q-layout>

</template>

<script setup>
import Navbar from 'src/components/Navbar.vue';
import FooterAdd from 'src/components/FooterAdd.vue';
import { inject } from 'vue';
import  Drawerleft  from 'src/components/DrawerLeft.vue';
import DrawerRight from 'src/components/DrawerRight.vue';
import {useQuasar} from 'quasar'
const userGoogle= inject('userGoogle')
const $q = useQuasar()


</script>
