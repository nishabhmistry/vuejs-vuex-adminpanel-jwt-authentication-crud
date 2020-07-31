<template>
  <div class="container">  
      <form @submit="formSubmit">

          <table border="1">
              <tr>
                  <td>Name:</td>
                  <td>
                      <input type="text" class="form-control" v-model="name" required>
                      <i v-if="output.message && output.message.name">
                        <br>
                        <i v-for="err in output.message.name">
                          {{err}}<br>
                        </i>
                      </i>
                  </td>
              </tr>
              <tr>
                  <td>Strip:</td>
                  <td>
                      <input type="text" class="form-control" v-model="strip" required>
                      <i v-if="output.message && output.message.strip">
                        <br>
                        <i v-for="err in output.message.strip">
                          {{err}}<br>
                        </i>
                      </i>
                  </td>
              </tr>
              <tr>
                  <td colspan="2"><button class="btn btn-success">Submit</button></td>
              </tr>
          </table>
      </form>
      <strong>Output:</strong>
      <pre>
        {{output}}
      </pre>
    </div>
</template>

<script>
import axios from 'axios';

export default {

  data() {
    return {
      name: "",
      strip: "",
      league: "",
      leagues: "",
      output: ""
    };
  },

  methods: {

    getTeam() {
      let self = this;
      let leagueid = this.$route.params.leagueid;
      let teamid = this.$route.params.teamid;
      
      axios.get('{api url}/'+leagueid+'/teams/'+teamid)
      .then(function (response) {
        self.name = response.data[0].name;
        self.strip = response.data[0].strip;
        self.league = response.data[0].leagueid;
      })
      .catch(function (error) {
        self.output = error;
      });
    },

    formSubmit(e) {
      let self = this;
      let leagueid = this.$route.params.leagueid;
      let teamid = this.$route.params.teamid;
      e.preventDefault();
      
      axios.put('{api url}/'+leagueid+'/teams/'+teamid, {
        name: this.name,
        strip: this.strip
      })
      .then(function (response) {
        self.output = response.data;
        if(response.data.code == 200){
          self.$router.push('/team/list/'+leagueid);
        }
      })
      .catch(function (error) {
        self.output = error;
      });
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