<template>
  <div class="team-list">
      <nav>
          <router-link :to="`/team/create/${leagueid}`">Create</router-link>
      </nav>

      <table border="1">
         <tr>
            <th>Team Name</th>
            <th>Strip</th>
            <th>Action</th>
         </tr>
         <tr v-for="teams of team">
            <td>{{teams.name}}</td>
            <td>{{teams.strip}}</td>
            <td>
                <router-link :to="`/team/${leagueid}/edit/${teams.id}`">Edit</router-link>
                <button @click="deleteData(teams.id)">Delete</button>
            </td>
         </tr>
      </table>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'team-list',

  data() {
    return {
      team: [],
      leagueid: []
    };
  },

  methods: {
      deleteData: function(id) {
      
          axios.delete('{api url}/teams/'+id)
          .then(resp => {
              this.getTeam();
              console.log(resp.data);
          })
          .catch(error => {
              console.log(error);
          })
      },
      getTeam(){
        this.leagueid = this.$route.params.leagueid;

        axios.get('{api url}/'+this.leagueid+'/teams/')
        .then(response => {
            this.team = response.data
        })
        .catch(e => {
            this.errors.push(e)
        }) 
      }
  },


  created() {
    this.getTeam();
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