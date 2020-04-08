<!--This component is to render the list of exhibitors in the form of cards -->
<template>
    <div>
        <ul class="list-unstyled exhibitors-list">
            <li v-for="exhibitor in exhibitors" :key="exhibitor.id_exhibitor">
                <header class="exhibitor-card-header">
                    <div class="exhibitor-logo-container">
                        <img :src="exhibitor.logo" :alt="exhibitor.company_name" />
                    </div>
                </header>
                <div class="exhibitor-name">
                    <a @click="getExhibitor(exhibitor.id_exhibitor)">
                        <h3>{{exhibitor.company_name}}</h3>
                    </a>
                </div>
                <div class="exhibitor-body">
                    <!-- Conditional Render Booth based on if booth exist in an exhibitor or not -->
                    <a v-if="exhibitor.booth" class="exhibitor-booth" href="#">{{exhibitor.booth}}</a>

                    <a v-if="!exhibitor.booth" class="exhibitor-booth no-booth" href="#">No Booth</a>
                </div>
                <div class="exhibitor-button-area">
                    

                    <!-- Conditional Render Message with notif or without notide based on value of messaged in exhibitor -->
                    <a v-if="exhibitor.messaged !== 0" class="message active" title="message" v-on:click="openMessage(exhibitor.id_exhibitor)">
                        <div class="icon message-icon"></div>
                        <p>Messaged</p>
                    </a>
                    <a v-if="exhibitor.messaged === 0" class="message" title="message" v-on:click="openMessage(exhibitor.id_exhibitor)">
                        <div class="icon message-icon"></div>
                        <p>Message</p>
                    </a>

                    <!-- Conditional Render Bookmark based on if bookmark have value in exhibitor or not -->
                    <a v-if="exhibitor.bookmark !== 0" class="bookmark active" title="bookmarked" v-on:click="bookmark(exhibitor.id_exhibitor)">
                        <div class="icon bookmark-icon"></div>
                        <p>Bookmark</p>
                    </a>
                    <a v-if="exhibitor.bookmark === 0" class="bookmark" title="bookmark" v-on:click="bookmark(exhibitor.id_exhibitor)">
                        <div class="icon bookmark-icon"></div>
                        <p>Bookmark</p>
                    </a>
                </div>
            </li>
        </ul>
        <ExhibitorModal v-if="showExhibitorModal" :exhibitor="findExhibitor" :showExhibitorModal="showExhibitorModal" @close="showExhibitorModal = false" @bookmark="bookmark" @openMessage="openMessage"/>

        <MessageModal v-if="showMessageModal" @close="showMessageModal = false; isMessageSubmitted = false" :isMessageSubmitted="isMessageSubmitted" :exhibitor="findExhibitor" @submitMessage="submitMessage"/>
    </div>
</template>

<script>
  // @ is an alias to /src
  import axios from 'axios';
  import {client_id } from '../variables.js';
  import ExhibitorModal from "./ExhibitorModal.vue";
  import MessageModal from "./MessageModal.vue";

  export default {
      name: 'ExhibitorCard',
      props: ['exhibitors'],
      components: {
          ExhibitorModal,
          MessageModal
      },
      data() {
          return {
              //showExhibitorModal is indicator Exhibitor modal is opened or not
              showExhibitorModal: false,
              //an indicator MessageModal is opened or not
              showMessageModal: false,
              //the result of get exhibitor by id_exhibitor
              findExhibitor : [],
              //the state of is Message submitted or not
              isMessageSubmitted: 0,
          }
      },
      methods: {
        //getExhibitor is a function to open the exhibitor modal, then retrieve the data of exhibitor based on the id_exhibitor
        getExhibitor: function(key){
            this.showExhibitorModal = true;
            this.findExhibitor = this.exhibitors.find(exhibitor =>
            exhibitor.id_exhibitor == key)
        },
        //bookmark is a function to change the status of the item, whether it will be bookmarked or not
        bookmark: function (key) {
            //Find index of specific object using findIndex method.    
            let objIndex = this.exhibitors.findIndex((obj => obj.id_exhibitor == key));

            //Update object's bookmark property, if bookmark = 0 update it with client_id, if not update it back to 0.
            if(!this.exhibitors[objIndex].bookmark) {
                this.exhibitors[objIndex].bookmark = client_id
            } else {
                this.exhibitors[objIndex].bookmark = 0
            }
        },

        //openMessage is a function to open the message modal
        openMessage: function (key) {
            if(this.showExhibitorModal) {
                this.showExhibitorModal = false
            }
            this.showMessageModal = true;
            this.findExhibitor = this.exhibitors.find(exhibitor =>
            exhibitor.id_exhibitor == key)
        },

        //submitMessage is a function to message the exhibitor. Since this is a prototype, then it is just changing the status of the message
        submitMessage: function(key) {
            //Find index of specific object using findIndex method.    
            let objIndex = this.exhibitors.findIndex((obj => obj.id_exhibitor == key));

            //Update object's bookmark property, if bookmark = 0 update it with client_id, if not update it back to 0.
            if(!this.exhibitors[objIndex].messaged) {
                this.exhibitors[objIndex].messaged = 1
            } 
            this.isMessageSubmitted = true;
        }
      }
  }
</script>