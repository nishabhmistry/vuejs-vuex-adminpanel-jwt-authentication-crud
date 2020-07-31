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
                <h1 class="h4 text-gray-900 mb-4">Login!</h1>
              </div>
              <form class="login" @submit.prevent="login">

              	<p v-if="errors.length">
                  <b>Please correct the following error(s):</b>
                  <ul>
                    <li v-for="error in errors">{{ error }}</li>
                  </ul>
                </p>

                <div class="form-group">
                  <input class="form-control form-control-user" type="text" v-model="username" placeholder="Username">
                </div>
                <div class="form-group">
                  <input class="form-control form-control-user" v-model="password" type="password" placeholder="Password">
                </div>
                <button class="btn btn-primary btn-user btn-block">Login</button>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
 <!--<div>
   <form class="login" @submit.prevent="login">
     <h1>Sign in</h1>
     <table border="1">
        <tr>
            <td>Username:</td>
            <td><input required v-model="username" type="username" placeholder="Username"/></td>
          </tr>
          <tr>
            <td>Password:</td>
            <td><input required v-model="password" type="password" placeholder="Password"/></td>
          </tr>
          <tr>
            <td colspan="2"><button type="submit">Login</button></td>
          </tr>
        </table>
   </form>
 </div>-->
</template>

<script>
import Header from './Header.vue';
import Vue from 'vue';
import VueToast from 'vue-toast-notification';
import 'vue-toast-notification/dist/theme-default.css';

Vue.use(VueToast);
export default {
	data(){
      	return {
        	username : "",
        	password : "",
        	errors: []
      	}
    },
    component(){
        Header
    },
    methods: {
        login: function (e) {

        	let username = this.username; 
            let password = this.password;

            this.errors = [];
        	if (!username) {
              	this.errors.push('Username required.');
          	} if (!password) {
              	this.errors.push('Password required.');
          	}

        	this.$store.dispatch('login', { username, password })
            .then((res) => 
            	this.$router.push({ path: '/admin/index' })
            )
            .catch(err => 
            	console.log("NND"+err)
            )
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