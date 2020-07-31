<template>
  <div class="league-list">
      <nav>
          <router-link to='/league/create'>Create</router-link>
      </nav>

      <table border="1">
         <tr v-for="leagues of league">
            <td>{{leagues.name}}</td>
            <td><router-link :to="`/team/list/${leagues.id}`">List</router-link></td>
            <td><router-link :to="`/league/edit/${leagues.id}`">Edit</router-link></td>
         </tr>
      </table>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'league-list',

  data() {
    return {
      league: [],
      league1: ""
    };
  },

  created() {
    
    axios.get('{api url}/leagues')
    .then(response => {
      this.league = response.data
    })
    .catch(e => {
      this.errors.push(e)
    })
  }
}
</script>
<style>
table, th, td { 
    border: 1px solid black; 
    border-collapse: collapse; 
} 
  
th, td { 
    padding: 20px; 
} 
  
th { 
    text-align: left; 
}
</style>