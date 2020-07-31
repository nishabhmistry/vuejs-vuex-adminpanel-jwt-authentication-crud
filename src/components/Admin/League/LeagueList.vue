<template>
        
        <div class="container-fluid">

        	<div class="d-sm-flex align-items-center justify-content-between mb-4">
            	<h1 class="h3 mb-0 text-gray-800">Leagues</h1>
            	<router-link class="d-none d-sm-inline-block btn btn-sm btn-primary shadow-sm" to='league/create'>
          			Create
        		</router-link>
          </div>
          
          
          <div class="card shadow mb-4">
            <div class="card-header py-3">
              <h6 class="m-0 font-weight-bold text-primary">List</h6>
            </div>
            <div class="card-body">
              <div class="table-responsive">
                <table class="table table-bordered" width="100%" cellspacing="0">
                  <thead>
                    <tr>
                      <th>ID</th>
                      <th>Name</th>
                      <th>Created at</th>
                      <th>Action</th>
                    </tr>
                  </thead>
                  <tfoot>
                    <tr>
                      <th>ID</th>
                      <th>Name</th>
                      <th>Created at</th>
                      <th>Action</th>
                    </tr>
                  </tfoot>
                  <tbody>
                    <tr v-for="leagues of league">
      			            <td>{{leagues.id}}</td>
      			            <td>{{leagues.name}}</td>
      			            <td>{{leagues.created_at.date}}</td>
      			            <td><router-link :to="`/admin/league/edit/${leagues.id}`">Edit</router-link></td>
      			        </tr>
                  </tbody>
                </table>
              </div>
            </div>
          </div>

        </div>
        
      
      

  
</template>

<script>
import axios from 'axios';
import Sidebar from './../Sidebar.vue';
import Header from './../Header.vue';
import Index from './../Index.vue';
import Footer from './../Footer.vue';

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
