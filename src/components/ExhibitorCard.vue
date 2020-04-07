<!--This component is to render the list of exhibitors in the form of cards -->
<template>
    <ul class="list-unstyled exhibitors-list">
        <li v-for="exhibitor in exhibitors" :key="exhibitor.id_exhibitor">
            <header class="exhibitor-card-header">
                <div class="exhibitor-logo-container">
                    <img :src="exhibitor.logo" :alt="exhibitor.company_name" />

                    
                </div>
            </header>
            <div class="exhibitor-name">
                <h3>{{exhibitor.company_name}}</h3>
            </div>
            <div class="exhibitor-body">
                <!-- Conditional Render Booth based on if booth exist in an exhibitor or not -->
                <a v-if="exhibitor.booth" class="exhibitor-booth" href="#">{{exhibitor.booth}}</a>

                <a v-if="!exhibitor.booth" class="exhibitor-booth no-booth" href="#">No Booth</a>

                
            </div>
            <div class="exhibitor-button-area">
                

                <!-- Conditional Render Message with notif or without notide based on value of messaged in exhibitor -->
                <a v-if="exhibitor.messaged !== 0" class="message active" title="message" v-on:click="message(exhibitor.id_exhibitor)">
                    <div class="icon message-icon"></div>
                    <p>Messaged</p>
                </a>
                <a v-if="exhibitor.messaged === 0" class="message" title="message" v-on:click="message(exhibitor.id_exhibitor)">
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
</template>

<script>
  // @ is an alias to /src
  import axios from 'axios';
  import {client_id } from '../variables.js'

  export default {
      name: 'ExhibitorCard',
      props: ['exhibitors'],
      methods: {
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

        //bookmark is a function to change the status of the item, whether it will be bookmarked or not
        message: function (key) {
            //Find index of specific object using findIndex method.    
            let objIndex = this.exhibitors.findIndex((obj => obj.id_exhibitor == key));

            //Update object's messaged property, if message = 0 update it with 1, if not update it back to 0.
            if(!this.exhibitors[objIndex].messaged) {
                this.exhibitors[objIndex].messaged = 1
            } else {
                this.exhibitors[objIndex].messaged = 0
            }
        }
      }
  }
</script>