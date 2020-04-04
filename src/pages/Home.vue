<template>
  <div class="home">
    <header class="nav-header">
      <div class="container">
          <input class="search-box" type="text" v-model="search" placeholder="Search Exhibitor..." />
      </div>
    </header>
    <div class="content">
      <div class="container">
          <ExhibitorCard v-if="!search" :exhibitors="filteredExhibitors" />

          <ExhibitorCard v-if="search" :exhibitors="filteredExhibitorsBySearch" />
      </div>
    </div>
  </div>
</template>

<script>
  // @ is an alias to /src
  import axios from 'axios';
  import ExhibitorCard from '../components/ExhibitorCard.vue';
  const event_id = "1b59351267938da712d19d57889c7f565cab96406e27a874607b90492a2845232f233a2b72bb4ae006a79b53f95aef054935c50b64d6a2a03cfe5cc75cbcd5cd";
  const client_id = "45426";
  const apiUrl = `https://api.jublia.com/buzz/v2/directory/search?event_id=${event_id}&client_id=${client_id}`;

  export default {
    name: 'Home',
    components: {
        ExhibitorCard
    },
    data() {
      return {
        exhibitors : [],
        filteredExhibitors : [],
        search: '',
      }
    },

    //Fetch exhibitors with axios
    created() {

      axios.get(apiUrl)
        .then(response => {
          // JSON responses are automatically parsed.
          this.exhibitors = response.data.searchResult;
          this.filteredExhibitors = this.exhibitors.slice(0,12);
        })
    },
    mounted() {
      
    },
    computed: {
      filteredExhibitorsBySearch() {
        return this.exhibitors
          .filter(exhibitor =>
            exhibitor.company_name.toLowerCase().includes(this.search.toLowerCase())
          )
      }
    }
  }
</script>