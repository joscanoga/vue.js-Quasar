<script setup>
  import { inject } from 'vue'
  const leftDrawerOpen = inject('leftDrawerOpen')

</script>



<template>
  <q-drawer show-if-above v-model="leftDrawerOpen" side="left" bordered>
    <!-- drawer content -->
  </q-drawer>
</template>


<style scoped>
</style>
