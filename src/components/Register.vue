<template>
<div>
<Header />
<div class="container">

    <div class="card o-hidden border-0 shadow-lg my-5">
      <div class="card-body p-0">
        
        <div class="row">
          <div class="col-lg-5 d-none d-lg-block bg-register-image"></div>
          <div class="col-lg-7">
            <div class="p-5">
              <div class="text-center">
                <h1 class="h4 text-gray-900 mb-4">Create an Account!</h1>
              </div>
              <form @submit="formSubmit" class="user">

                <p v-if="errors.length">
                  <b>Please correct the following error(s):</b>
                  <ul>
                    <li v-for="error in errors">{{ error }}</li>
                  </ul>
                </p>

                <div class="form-group row">
                  <div class="col-sm-6 mb-3 mb-sm-0">
                    <input type="text" class="form-control form-control-user" id="exampleFirstName" placeholder="First Name" v-model="firstname">
                  </div>
                  <div class="col-sm-6">
                    <input type="text" class="form-control form-control-user" id="exampleLastName" placeholder="Last Name" v-model="lastname">
                  </div>
                </div>

                <div class="form-group">
                  <input class="form-control form-control-user" type="text" v-model="email" placeholder="Email">
                </div>
                <div class="form-group">
                  <input class="form-control form-control-user" type="text" v-model="username" placeholder="Username">
                </div>
                <div class="form-group">
                  <input class="form-control form-control-user" type="password" v-model="password" placeholder="Password">
                </div>
                <!--<div class="file-field">
                    <div class="btn btn-primary btn-sm float-left">
                      <span>Choose file</span>
                      <input type="file">
                    </div>
                    <div class="file-path-wrapper">
                      <input class="file-path validate" type="text" placeholder="Upload your file">
                    </div>
                </div>-->

                <button class="btn btn-primary btn-user btn-block">Register</button>
              </form>
              <hr>
              <div class="text-center">
                  <router-link class="small" to='login'>
                      Already have an account? Login!
                  </router-link>
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
Vue.component('Header', function (resolve) {
  require(['./Header'], resolve)
})

export default {
    name: 'registration',

  	data() {
    	return {
      		firstname: "",
          lastname: "",
          email: "",
          username: "",
      		password: "",
      		output: "",
          errors: []
    	};
  	},
    component(){
        BToast
    },
  	methods: {
    	formSubmit(e) {
          e.preventDefault();
      		let self = this;

          this.errors = [];

          if (!this.firstname) {
              this.errors.push('Firstname required.');
          } else if (this.firstname.length < 3 || this.firstname.length > 20) {
              this.errors.push('Firstname length between 3 and 20.');
          } if (!this.lastname) {
              this.errors.push('Lastname required.');
          } else if (this.lastname.length < 3 || this.lastname.length > 20) {
              this.errors.push('Lastname length between 3 and 20.');
          } if (!this.email) {
              this.errors.push('Email required.');
          } else if (!this.validEmail(this.email)) {
              this.errors.push('Valid email required.');
          } if (!this.username) {
              this.errors.push('Username required.');
          } else if (this.username.length < 3 || this.username.length > 15) {
              this.errors.push('Lastname length between 3 and 15.');
          } if (!this.password) {
              this.errors.push('Password required.');
          }
      		
          if(!this.errors.length){
          		axios.post('{base url}/api/register', {
            		firstname: this.firstname,
                lastname: this.lastname,
                email: this.email,
                username: this.username,
            		password: this.password
          		})
          		.then(function (response) {
                  Vue.$toast.open({
                      message: response.data.message,
                      type: "success",
                      duration: 10000,
                      dismissible: true,
                      position: "top-right"
                  });
          			  self.output = response.data.message;
          			  if(response.data.code == 200){
          				    self.$router.push('/login');
          			  }
          		})
          		.catch(function (error) {
            		self.output = error;
          		});
          }
    	},
      validEmail: function (email) {
        var re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
        return re.test(email);
      }
  	}
}
</script>