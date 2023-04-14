<script setup>
  import { inject } from 'vue'
  const rightDrawerOpen = inject('rightDrawerOpen')

</script>

<template>
  <q-drawer show-if-above v-model="rightDrawerOpen" side="right" bordered>
      <!-- drawer content -->
    </q-drawer>
</template>


<style scoped>
</style>
