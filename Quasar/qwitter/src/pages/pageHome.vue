<script setup>
import { formatDistance } from 'date-fns'
import { filter } from 'compression';
import { collection, query, onSnapshot, orderBy, limit, doc, deleteDoc } from "firebase/firestore";
import inputQweet from 'src/components/inputQweet.vue';
import { db } from "../firebase"
import { inject, ref, watchEffect } from 'vue'
const userGoogle = inject('userGoogle')

const relativeDate = (date) => formatDistance(date, new Date())

const deleteQweet = (qweet) => {
  const id = qweet.id
  deleteDoc(doc(db, "Qweets", id));

}
const Qweets = ref([])

//watchEffect es un metodo similar a un useEffect de react js


const q = query(collection(db, "Qweets"),orderBy("time" ),limit(20));
const unsubscribe = onSnapshot(q, (snapshot) => {
  snapshot.docChanges().forEach((change) => {
    let qweetChange=change.doc.data();
    if (change.type === "added") {

        Qweets.value.unshift({
            id: change.doc.id,
            //trae los datos del documento y los guarda en el objeto actual
            ...change.doc.data()
          });

    }
    if (change.type === "modified") {
        console.log("Modified : ", change.doc.data());
    }
    if (change.type === "removed") {
        let index=Qweets.value.findIndex(qweet => qweet.id === change.doc.id)
        Qweets.value.splice(index, 1)
    }
  });
});

</script>

<template>
  <q-page>
    <inputQweet v-show="userGoogle" />
    <q-separator class="divider" size="10px" color="grey-2" />
    <div class="qweetsArea ">
      <q-scroll-area class="" :thumb-style="thumbStyle" :bar-style="barStyle" style="height: 82vh; max-width: 1500px;">
        <q-list separator class="rounded-borders" style="">

          <transition-group appear enter-active-class="animated fadeIn slow" leave-active-class="animated fadeOut slow">

            <q-item v-for="qweet in Qweets" :key="qweet.time" class="qweet q-py-md">
              <q-item-section avatar top>
                <q-avatar>
                  <img src="https://cdn.quasar.dev/img/avatar2.jpg">
                </q-avatar>
              </q-item-section>

              <q-item-section>
                <q-item-label class="text-subtitle1">
                  <strong>
                    {{qweet.displayName}}
                  </strong>
                  <span class="text-gyey-7">
                    @{{ qweet.displayName.trim().replace(/\s+/g, '')}}
                  </span>
                  <br class="lt-md">&bull;{{ relativeDate(qweet.time) }}
                </q-item-label>
                <q-item-label class="qweet-content text-body1">
                  {{qweet.QweetContent}}
                </q-item-label>
                <div class="qweet-icons row justify-between q-mt-sm">
                  <q-btn color="grey" icon="comment" flat round size="sm"></q-btn>
                  <q-btn color="grey" icon="fa fa-retweet" flat round size="sm"></q-btn>
                  <q-btn color="grey" icon="far fa-heart" flat round size="sm"></q-btn>
                  <q-btn @click="deleteQweet(qweet)"  v-show="qweet.uid==userGoogle.uid" color="grey" icon="fa fa-trash" flat round size="sm"></q-btn>
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

