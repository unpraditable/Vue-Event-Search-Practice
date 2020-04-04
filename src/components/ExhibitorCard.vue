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
                <a class="exhibitor-booth" href="#">{{exhibitor.booth}}</a>
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