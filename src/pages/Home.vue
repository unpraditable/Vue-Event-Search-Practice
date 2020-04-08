<template>
  <div class="home">
    <header class="nav-header">
      <div class="container">
          <input class="search-box" type="text" v-model="search" placeholder="Search Exhibitor..." />
          
      </div>
    </header>
    <div class="content">
      <div class="container">
        <ul class="list-unstyled filter-list">
              <li>
                <a class="active" data-value="all" v-on:click="filterIndex"> ALL</a>
              </li>
              <li v-for="filter in filterList" :key="filter.name">
                  <a v-bind:data-value="filter.value" v-on:click="filterIndex">{{filter.name}}</a>
              </li>
          </ul>
        <!-- If there is no search parameter, return whole exhibitors data -->
          <ExhibitorCard v-if="!isFiltered && !search" :exhibitors="exhibitors" />

          <!-- if there is a filter, return filter exhibitor data -->
          <ExhibitorCard v-if="isFiltered && !search" :exhibitors="filteredExhibitors" />

          <!-- it there is a search parameter, return filtered exhibitor data by search -->
          <ExhibitorCard v-if="search" :exhibitors="filteredExhibitorsBySearch" />

          <p v-if="(search && filteredExhibitorsBySearch.length ===0) || (isFiltered && filteredExhibitors.length ===0)">
            No Exhibitor Found!
          </p>
      </div>
    </div>
  </div>
</template>

<script>
  // import axios
  import axios from 'axios';
  // import Exhibitor Card component
  import ExhibitorCard from '../components/ExhibitorCard.vue';
  import { event_id, client_id, apiUrl } from '../variables.js'


  export default {
    name: 'Home',
    components: {
        ExhibitorCard,
    },
    data() {
      return {
        //exhibitors is a data of exhibitors without filter
        exhibitors : [],
        //filteredExhibitors is a data of exhibitors with filters
        filteredExhibitors : [],
        //search is a keyword that being used as a search parameters
        search: '',
        //filterList is a list of filter components in navigation
        filterList: [
            {
                name: "0-9",
                value: "numbers"
            }
        ],
        isFiltered: false,

      }
    },

    created() {

      if (localStorage.getItem('exhibitors')) {
          //if there is an item in localstorage, then set exhibitor to localstorage
          this.exhibitors = JSON.parse(localStorage.getItem('exhibitors'))
        } else {
          //if there is no item in localstorage, fetch the exhibitors from the API
          axios({
            method: 'get',
            url: apiUrl,
            params: {
              event_id: event_id,
              client_id: client_id
            }
          })
          .then(response => {
            this.exhibitors = response.data.searchResult;
          })
      };
      
      //Push all alphabets to filterList
      let alphabets = "abcdefghijklmnopqrstuvwxyz";
      for(let i=0;i<alphabets.length;i++){
          this.filterList.push({"name": alphabets[i].toUpperCase(), "value": alphabets[i]});
      }
      
    },
    computed: {
      // filteredExhibitorBySearch() is a function to return a search result exhibitor by real time
      filteredExhibitorsBySearch() {
        let exhibitors = "";
        if(this.isFiltered) {
          exhibitors = this.filteredExhibitors
        } else {
          exhibitors = this.exhibitors;
        }
        return exhibitors
          .filter(exhibitor =>
            exhibitor.company_name.toLowerCase().includes(this.search.toLowerCase())
          )
      }
    },
    watch: {
      exhibitors: {
        handler() {
          //everytime exhibitors is changed from any triggers, like bookmark button or message button, update the local storage too 
          localStorage.setItem('exhibitors', JSON.stringify(this.exhibitors));
        },
        deep: true,
      },
    },
    methods: {
      //filterIndex is a function to filter exhibitor based on the first character of the items
      filterIndex: function (event) {
        // `event` is the native DOM event
        let value = event.target.getAttribute("data-value");

        //find active elements of the filter element, then remove the active class
        let activeEl = document.querySelector(".filter-list .active");
        activeEl.classList.remove("active");

        //find the clicked element, the add the active class
        event.target.classList.add("active");

        //if the filter is all, return the filtered exhibitors list
        if(value != "all") {
          this.isFiltered = true;
          //if the first character is numerical, execute this function
          if(value == "numbers"){
            this.filteredExhibitors = this.exhibitors
            .filter(exhibitor =>
               Number.isInteger(
                 parseInt(exhibitor.company_name[0].toLowerCase()))
              )
          } else {
            //if the first character is not numerical, execute this
            this.filteredExhibitors = this.exhibitors
            .filter(exhibitor =>
              exhibitor.company_name[0].toLowerCase() == value)
            }
        } else {
          //return all exhibitors if all filter is activated
          this.isFiltered = false;
        }
      },
      
    }
  }
</script>