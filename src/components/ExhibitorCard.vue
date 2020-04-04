<template>
    <ul class="list-unstyled exhibitors-list">
        <li v-for="exhibitor in exhibitors" :key="exhibitor.id_exhibitor">
            <div class="exhibitor-logo-container">
            <img :src="exhibitor.logo" />
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