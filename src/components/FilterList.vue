<template>
    <ul class="list-unstyled filter-list">
        <li v-for="filter in filterList" :key="filter.name">
            <a>{{filter.name}}</a>
        </li>
    </ul>
</template>

<script>
    export default{
        name: 'FilterList',
        data() {
            return{
                //filterList is a list of filter components in navigation
                filterList: [
                    {
                        name: "ALL",
                        value: "all"
                    },
                    {
                        name: "0-9",
                        value: "numbers"
                    }
                ]
            }
        },
        created() {
            //Push all alphabets to filterList
            let alphabets = "abcdefghijklmnopqrstuvwxyz";
            for(let i=0;i<alphabets.length;i++){
                this.filterList.push({"name": alphabets[i].toUpperCase(), "value": alphabets[i]});
            }
        }
    }
</script>