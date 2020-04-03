<template>
  <div class="home">
    <header>
      <div class="container">
        
      </div>
    </header>
    <div class="content">
      <div class="container">
          <ul class="list-unstyled exhibitors-list">
              <li v-for="exhibitor in exhibitors" :key="exhibitor.id_exhibitor">
                  <div class="exhibitor-logo-container">
                    <img :src="exhibitor.logo" />
                  </div>
              </li>
          </ul>
      </div>
    </div>
  </div>
</template>

<script>
  // @ is an alias to /src
  import axios from 'axios';
  const event_id = "1b59351267938da712d19d57889c7f565cab96406e27a874607b90492a2845232f233a2b72bb4ae006a79b53f95aef054935c50b64d6a2a03cfe5cc75cbcd5cd";
  const client_id = "45426";
  const apiUrl = `https://api.jublia.com/buzz/v2/directory/search?event_id=${event_id}&client_id=${client_id}`;

  export default {
    name: 'Home',
    data() {
      return {
        exhibitors : []
      }
    },

    //Fetch exhibitors with axios
    created() {

      axios.get(apiUrl)
        .then(response => {
          // JSON responses are automatically parsed.
          this.exhibitors = response.data.searchResult;

        })
        .catch(e => {
          this.countries.push(e)
        })
    },
    mounted() {
      
    },
    computed: {
      
    }
  }
</script>