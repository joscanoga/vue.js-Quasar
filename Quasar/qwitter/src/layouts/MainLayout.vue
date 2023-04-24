<script setup>
import { ref } from 'vue'
import { inject } from 'vue';
import navbar from 'src/components/navbar.vue';
import LeftDrawer from 'src/components/LeftDrawer.vue';
import RightDrawer from 'src/components/RightDrawer.vue';

</script>

<template>
  <q-layout view="lHr lpR fFf">
    <navbar/>
    <left-drawer/>
    <RightDrawer/>
    <q-page-container>
      <router-view />
    </q-page-container>

  </q-layout>
</template>

