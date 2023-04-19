<script setup>
import { computed, ref } from 'vue'
import { formatDistance } from 'date-fns'
import { filter } from 'compression';
const newQueetContent = ref('')
const relativeDate = (date) => formatDistance(date, new Date())
const addQweet = () => {
  qweets.value.push({
    content: newQueetContent.value,
    date: Date.now(),
    username: 'username',
    name: 'nombre usuario'
  })
  newQueetContent.value = ''
}
const deleteQweet = (qweet) => {
  const date = qweet.date
  const index = qweets.value.findIndex(qweet => qweet.date === date)
  qweets.value.splice(index, 1)

}
const qweets = ref([
  {
    content: "lorem ipsum dolor sit amet consectetur adipisicing elit. Distinctio, quaerat. Aspernatur, dolorum? Aliquam eaque dolorem earum, voluptatum, doloribus cumque harum, iure natus laboriosam rerum commodi reiciendis asperiores nulla adipisci accusamus.",
    date: 1681852799484,
    username: "username",
    name: "nombre usuario"
  },
  {
    content: "lorem ipsum dolor sit amet consectetur adipisicing elit. Distinctio, quaerat. Aspernatur, dolorum? Aliquam eaque dolorem earum, voluptatum, doloribus cumque harum, iure natus laboriosam rerum commodi reiciendis asperiores nulla adipisci accusamus.",
    date: 1681852799485,
    username: "username",
    name: "nombre usuario"
  },
  {
    content: "lorem ipsum dolor sit amet consectetur adipisicing elit. Distinctio, quaerat. Aspernatur, dolorum? Aliquam eaque dolorem earum, voluptatum, doloribus cumque harum, iure natus laboriosam rerum commodi reiciendis asperiores nulla adipisci accusamus.",
    date: 1681852799486,
    username: "username",
    name: "nombre usuario"
  },
])



</script>

<template>
  <q-page>


    <div class="q-py-lg q-px-md row items-end q-col-gutter-md">
      <div class="col  ">
        <q-input class="newQuweet" bottom-slots v-model="newQueetContent" placeholder="What's happening?" counter
          maxlength="250" autogrow @keyup.enter="addQweet" dense>
          <template v-slot:before>
            <q-avatar size="xl">
              <img src="https://cdn.quasar.dev/img/avatar5.jpg">
            </q-avatar>
          </template>
        </q-input>
      </div>
      <div class="col col-shrink">

        <q-btn @click="addQweet" unelevated rounded color="primary" label="Qweet" no-caps :disable="!newQueetContent" />

      </div>
    </div>
    <q-separator class="divider" size="10px" color="grey-2" />
    <div class="qweetsArea ">
      <q-scroll-area class="" :thumb-style="thumbStyle" :bar-style="barStyle" style="height: 82vh; max-width: 1500px;">
        <q-list separator class="rounded-borders" style="">

          <transition-group appear enter-active-class="animated fadeIn slow" leave-active-class="animated fadeOut slow">

            <q-item v-for="qweet in qweets" :key="qweet.date" class="qweet q-py-md">
              <q-item-section avatar top>
                <q-avatar>
                  <img src="https://cdn.quasar.dev/img/avatar2.jpg">
                </q-avatar>
              </q-item-section>

              <q-item-section>
                <q-item-label class="text-subtitle1">
                  <strong>
                    {{ qweet.name }}
                  </strong>
                  <span class="text-gyey-7">
                    @{{ qweet.username }}
                  </span>
                  <br class="lt-md">&bull;{{ relativeDate(qweet.date) }}
                </q-item-label>
                <q-item-label class="qweet-content text-body1">
                  {{ qweet.content }}
                </q-item-label>
                <div class="qweet-icons row justify-between q-mt-sm">
                  <q-btn color="grey" icon="comment" flat round size="sm"></q-btn>
                  <q-btn color="grey" icon="fa fa-retweet" flat round size="sm"></q-btn>
                  <q-btn color="grey" icon="far fa-heart" flat round size="sm"></q-btn>
                  <q-btn @click="deleteQweet" color="grey" icon="fa fa-trash" flat round size="sm"></q-btn>
                </div>
              </q-item-section>


            </q-item>
          </transition-group>

        </q-list>
      </q-scroll-area>
    </div>

  </q-page>
</template>
<style lang="sass" scoped>
.newQuweet
  max-width: 600px
  margin: 0 auto
  font-size: 18px
  textarea
    font-size: 19px
    line-height: 1.4 !important
.divider
  border-top: 1px solid
  border-bottom: 1px solid
  border-color: $grey-4
.qweet-content
  white-space: pre-line

.qweet-icons
  margin-left: -5px

.qweet:not(:first-child)
  border-top: 1px solid rgba(0,0,0,0.1)
</style>

