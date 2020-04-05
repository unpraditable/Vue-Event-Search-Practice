<template>
  <div class="home">
    <header class="nav-header">
      <div class="container">
          <input class="search-box" type="text" v-model="search" placeholder="Search Exhibitor..." />
          <FilterList />
      </div>
    </header>
    <div class="content">
      <div class="container">
        <!-- If there is no search parameter, return whole exhibitors data -->
          <ExhibitorCard v-if="!search" :exhibitors="exhibitors" />
        <!-- If there is a search parameter, return filtered exhibitors data by search -->
          <ExhibitorCard v-if="search" :exhibitors="filteredExhibitorsBySearch" />
      </div>
    </div>
  </div>
</template>

<script>
  // import axios
  import axios from 'axios';
  // import Exhibitor Card component
  import ExhibitorCard from '../components/ExhibitorCard.vue';
  // import Filter List component
  import FilterList from '../components/FilterList.vue';
  //store event_id and client_id params to a constant
  const event_id = "1b59351267938da712d19d57889c7f565cab96406e27a874607b90492a2845232f233a2b72bb4ae006a79b53f95aef054935c50b64d6a2a03cfe5cc75cbcd5cd";
  const client_id = "45426";
  //store apiUrl to a constant
  const apiUrl = `https://api.jublia.com/buzz/v2/directory/search?event_id=${event_id}&client_id=${client_id}`;

  export default {
    name: 'Home',
    components: {
        ExhibitorCard,
        FilterList
    },
    data() {
      return {
        //exhibitors is a data of exhibitors without filter
        exhibitors : [],
        //filteredExhibitors is a data of exhibitors with filters
        filteredExhibitors : [],
        //search is a keyword that being used as a search parameters
        search: '',
      }
    },

    created() {
      //Fetch exhibitors with axios when the component is created
      axios.get(apiUrl)
        .then(response => {
          // JSON responses are automatically parsed with axios
          this.exhibitors = response.data.searchResult;
          this.filteredExhibitors = this.exhibitors.slice(0,12);
        })
    },
    mounted() {
      
    },
    computed: {
      // filteredExhibitorBySearch() is a function to return a search result exhibitor by real time
      filteredExhibitorsBySearch() {
        return this.exhibitors
          .filter(exhibitor =>
            exhibitor.company_name.toLowerCase().includes(this.search.toLowerCase())
          )
      }
    }
  }
</script>