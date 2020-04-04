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
                <a v-if="exhibitor.booth" class="exhibitor-booth" href="#">{{exhibitor.booth}}</a>
                <a v-if="!exhibitor.booth" class="exhibitor-booth no-booth" href="#">No Booth</a>

                <a v-if="exhibitor.bookmark !=0" class="bookmarked">
                    <span class="icon bookmark-icon active"></span>
                    Bookmarked
                </a>
                <a v-if="exhibitor.bookmark ===0" class="bookmark">
                    <span class="icon bookmark-icon"></span>
                    Bookmark
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