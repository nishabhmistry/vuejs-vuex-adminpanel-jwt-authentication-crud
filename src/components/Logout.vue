<template>
  <div>
 </div>
</template>

<script>
import Vue from 'vue';
import VueToast from 'vue-toast-notification';
import 'vue-toast-notification/dist/theme-default.css';

Vue.use(VueToast);
export default {
	data(){
      	return {
      	}
    },
    created(){
        this.logout();
    },
    methods: {
        logout: function (e) {

        	   this.$store.dispatch('logout')
                .then((res) => 
            	     
                    Vue.$toast.open({
                        message: "Logged out successfully.",
                        type: "success",
                        duration: 10000,
                        dismissible: true,
                        position: "top-right"
                    }),
            	      this.$router.push('/login')
                )
                .catch(err => 
            	       console.log("NND"+err)
                )
        }
    }
}
</script>