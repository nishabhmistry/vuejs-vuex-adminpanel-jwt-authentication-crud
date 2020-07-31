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
  name: 'league-create',

  data() {
    return {
      name: "",
      strip: "",
      league: "",
      leagues: "",
      currentleague: "",
      output: ""
    };
  },

  methods: {
    formSubmit(e) {
      let self = this;
      let id = this.$route.params.leagueid;
      //let leagueid = this.league;
      e.preventDefault();
      
      axios.post('{api url}/'+id+'/teams', {
        name: this.name,
        strip: this.strip
      })
      .then(function (response) {
        self.output = response.data;
        if(response.data.code == 200){
          self.$router.push('/team/list/'+id);
        }
      })
      .catch(function (error) {
        self.output = error;
      });
    }
  },

  created(){
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