<template>
  <q-page >
      <div class="q-py-lg q-px-md row items-end q-col-gutter-md">
        <div class="col">
          <q-input
              v-model="newQweetContent"
              placeholder="what's happening?"
              class="new-qweet"
              bottom-slots
              autogrow
              counter maxlength="280"
              >
          <template v-slot:before>
             <q-avatar size="xl">
               <img src="Omar.jpg">
             </q-avatar>
           </template>
         </q-input>
        </div>
        <div class="col col-shrink">
            <q-btn
                @click="addNewQweet()"
                :disable="!newQweetContent"
                class="q-mb-lg"
                unelevated
                rounded
                no-caps
                color="primary"
                label="Qweet" />
        </div>
      </div>
      <q-separator
          class="divider"
          size="10px"
          color="grey-2"/>

  <q-list separator>
    
  <transition-group
  appear
  enter-active-class="animated fadeIn"
  leave-active-class="animated fadeOut"
>
<q-item
v-for="qweet in qweets"
:key="qweet.date"
class="q-py-md" >
  <q-item-section avatar top>
    <q-avatar>
      <img src="Omar.jpg">
    </q-avatar>
  </q-item-section>

  <q-item-section>
    <q-item-label  class="text-subtitle1">
     <strong>Omar Saeed</strong>
     <span class="text-grey-7 q-ml-xs">@omar</span>
    </q-item-label>
    <q-item-label  class="qweet-content text-body1">
    {{ qweet.content }}
    </q-item-label>
    <div class="qweet-icons row justify-between q-mt-sm">
        <q-btn
            flat
            round
            size="sm"
            color="grey"
            icon="far  fa-comment"
            />
        <q-btn
            flat
            round
            size="sm"
            color="grey"
            icon="fas fa-retweet"
            />
        <q-btn
            flat
            round
            size="sm"
            color="grey"
            icon="far fa-heart"
            />
        <q-btn
            @click="deleteQweet(qweet)"
            flat
            round
            size="sm"
            color="grey"
            icon="fas  fa-trash"
            />

    </div>
  </q-item-section>

  <q-item-section side top>
  {{ qweet.date  }}
  </q-item-section>
</q-item>

<q-separator inset="item" />
</transition-group>


    </q-list>
  </q-page>
</template>

<script>
import { date } from 'quasar'

export default {
  name: 'PageHome',
  data(){
     return {
        newQweetContent: '',
        qweets: [
          {
            content:  `Lorem ipsum dolor, sit amet consectetur adipisicing elit.
            Ipsam aspernatur corrupti quis provident magnam facere sint pariatur facilis,
            explicabo repellendus eaque. Odit ratione doloribus voluptatum cumque magni laborum deserunt quisquam?`,

            date: '30 minuted'
          },
          {
            content:  `Lorem ipsum dolor, sit amet consectetur adipisicing elit.
            Ipsam aspernatur corrupti quis provident magnam facere sint pariatur facilis,
            explicabo repellendus eaque. Odit ratione doloribus voluptatum cumque magni laborum deserunt quisquam?`,

            date: '20 minuted'
          },

        ]
     }
  },
   methods:{
    addNewQweet(){



      let newQweet= {
        content: this.newQweetContent,
        date: Date.now()
      }
      this.qweets.unshift(newQweet)
      this.newQweetContent=''

    },
    deleteQweet(qweet){
      let dateToDelete = qweet.date
      let index = this.qweets.findIndex(qweet =>qweet.date === dateToDelete)
      this.qweets.splice(index,1)
    }
   },



}
</script>

<style  lang="sass">
    .new-qweet
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
</style>
