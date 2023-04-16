<script setup>
  import { inject } from 'vue'
  import infoUser from 'src/components/infoUser.vue'
  const rightDrawerOpen = inject('rightDrawerOpen')

</script>

<template>
  <q-drawer show-if-above v-model="rightDrawerOpen" side="right" bordered>
      <info-user/>
    </q-drawer>
</template>


<style scoped>
</style>
