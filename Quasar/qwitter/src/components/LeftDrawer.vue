<script setup>
import { inject } from 'vue';
const leftDrawerOpen = inject('leftDrawerOpen')
</script>

<template>
  <q-drawer show-if-above v-model="leftDrawerOpen" side="left" bordered>
    <q-icon name="mdi-bird" class=" text-primary q-pa-md" size="md" />


    <q-list>
      <q-item clickable v-ripple to="/" exact>
        <q-item-section avatar>
          <q-icon color="primary" name="mdi-home" size="md" />
        </q-item-section>

        <q-item-section class="text-h6 text fa-weight-bold">Home</q-item-section>
      </q-item>
      <q-item to="/about" clickable v-ripple>
        <q-item-section avatar>
          <q-icon color="primary" name="mdi-information-variant" size="md" />
        </q-item-section>

        <q-item-section class="text-h6 text fa-weight-bold">About</q-item-section>
      </q-item>

    </q-list>


  </q-drawer>
</template>


<style scoped></style>
