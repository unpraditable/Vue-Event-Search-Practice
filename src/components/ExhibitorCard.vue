<template>
    <ul class="list-unstyled exhibitors-list">
        <li v-for="exhibitor in exhibitors" :key="exhibitor.id_exhibitor">
            <header class="exhibitor-card-header">
                <div class="exhibitor-logo-container">
                    <img :src="exhibitor.logo" :alt="exhibitor.company_name" />
                    <a v-if="exhibitor.bookmark !== 0" class="bookmark active" title="bookmarked">
                        <span class="icon bookmark-icon"></span>
                    </a>
                    <a v-if="exhibitor.bookmark === 0" class="bookmark" title="bookmark">
                        <span class="icon bookmark-icon"></span>
                    </a>
                </div>
            </header>
            <div class="exhibitor-name">
                <h3>{{exhibitor.company_name}}</h3>
            </div>
            <div class="exhibitor-body">
                <a v-if="exhibitor.booth" class="exhibitor-booth" href="#">{{exhibitor.booth}}</a>
                <a v-if="!exhibitor.booth" class="exhibitor-booth no-booth" href="#">No Booth</a>

                <a v-if="exhibitor.messaged !== 0" class="message active" title="message">
                    <span class="icon message-icon"></span>
                    Messaged
                </a>
                <a v-if="exhibitor.messaged === 0" class="message" title="message">
                    <span class="icon message-icon"></span>
                    Message
                </a>
            </div>
        </li>
    </ul>
</template>

<script>
  // @ is an alias to /src
  import axios from 'axios';

  export default {
      name: 'ExhibitorCard',
      props: ['exhibitors'],
  }
</script>