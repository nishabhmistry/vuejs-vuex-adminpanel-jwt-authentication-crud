<template>
  <div class="container">  
      <form @submit="formSubmit">
      	 <table>
            <tr>
                <td>Name:</td>
                <td>
                    <input type="text" class="form-control" v-model="name">
                    <i v-if="output.message">
                        <br>
                        <i v-for="err in output.message.name">
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
      output: ""
    };
  },

  methods: {

    getLeague() {
      let self = this;
      let id = this.$route.params.id;
      
      axios.get('{api url}/leagues/'+id)
      .then(function (response) {
        self.name = response.data[0].name;
      })
      .catch(function (error) {
        self.output = error;
      });
    },

    formSubmit(e) {
      let self = this;
      let id = this.$route.params.id;
      e.preventDefault();
      
      axios.put('{api url}/leagues/'+id, {
        name: this.name
      })
      .then(function (response) {
        self.output = response.data;
        //self.$router.push('/league/list');
      })
      .catch(function (error) {
        self.output = error;
      });
    }
  },

  created() {
      this.getLeague();
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