<template>
    <div class="container">  

    <div class="row justify-content-center">
      <div class="col-xl-10 col-lg-12 col-md-9">
        <div class="card o-hidden border-0 shadow-lg my-5">
          <div class="card-body p-0">
            
            <div class="row">
              <div class="col-lg-12">
                <div class="p-5">
                  <div class="text-center">
                    <h1 class="h4 text-gray-900 mb-4">Create League</h1>
                  </div>
                  <form class="user" @submit="formSubmit">
                    <p v-if="errors.length">
                      <b>Please correct the following error(s):</b>
                      <ul>
                        <li v-for="error in errors">{{ error }}</li>
                      </ul>
                    </p>
                    <div class="form-group">
                      <input type="text" class="form-control form-control-user" v-model="name" id="exampleInputEmail" aria-describedby="emailHelp" placeholder="Enter League Name">
                    </div>
                    <button class="btn btn-primary btn-user btn-block">Create</button>
                  </form>
                </div>
              </div>
            </div>
          </div>
        </div>

      </div>

    

  </div>
    </div>
</template>

<script>
import axios from 'axios';
import Vue from 'vue';
import VueToast from 'vue-toast-notification';
import 'vue-toast-notification/dist/theme-default.css';

Vue.use(VueToast);

export default {
  name: 'league-create',

  data() {
    return {
      name: "",
      output: "",
      errors: []
    };
  },
  component(){
      BToast
  },
  methods: {
    formSubmit(e) {
      let self = this;
      e.preventDefault();

      self.errors = [];
      if (!self.name) {
        self.errors.push('Name required.');
      }
      
      axios.post('{api url}/leagues', {
        name: this.name
      })
      .then(function (response) {
        self.output = response.data;
        if(response.data.code == 200){
          Vue.$toast.open({
              message: response.data.message,
              type: "success",
              duration: 10000,
              dismissible: true,
              position: "top-right"
          });
          self.$router.push('/admin/league');
        }
      })
      .catch(function (error) {
        self.output = error;
      });
    }
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