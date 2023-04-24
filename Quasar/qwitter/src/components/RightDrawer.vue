<script setup>
import { inject } from 'vue';
const rightDrawerOpen = inject('rightDrawerOpen')

</script>

<template>
  <q-drawer show-if-above v-model="rightDrawerOpen" side="right" bordered>
      <q-input class="q-ma-md" outlined rounded dense v-model="text" label="Search Qwitter">
        <template v-slot:prepend>
          <q-icon name="search" />
        </template>
      </q-input>
      <q-list separator padding>
        <q-item class="q-pa-md">
          <q-item-section>
            <q-item-label class="text-gray" overline>Education</q-item-label>
            <q-item-label>Something amazing</q-item-label>
            <q-item-label caption>Secondary line text. Lorem ipsum dolor sit amet, consectetur adipiscit
              elit.</q-item-label>
          </q-item-section>

          <q-item-section side top>
            <q-item-label caption>5 min ago</q-item-label>
          </q-item-section>
        </q-item>
        <q-item class="q-pa-md">
          <q-item-section>
            <q-item-label class="text-gray" overline>Education</q-item-label>
            <q-item-label>Something amazing</q-item-label>
            <q-item-label caption>Secondary line text. Lorem ipsum dolor sit amet, consectetur adipiscit
              elit.</q-item-label>
          </q-item-section>

          <q-item-section side top>
            <q-item-label caption>5 min ago</q-item-label>
          </q-item-section>
        </q-item>
        <q-item class="q-pa-md">
          <q-item-section>
            <q-item-label class="text-gray" overline>Education</q-item-label>
            <q-item-label>Something amazing</q-item-label>
            <q-item-label caption>Secondary line text. Lorem ipsum dolor sit amet, consectetur adipiscit
              elit.</q-item-label>
          </q-item-section>

          <q-item-section side top>
            <q-item-label caption>5 min ago</q-item-label>
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

</template>


<style scoped>

</style>
