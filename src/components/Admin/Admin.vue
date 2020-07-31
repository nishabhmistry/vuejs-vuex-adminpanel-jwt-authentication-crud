<template>
<html lang="en">
<body id="page-top">

  <div id="wrapper">

    <Sidebar></Sidebar>
    
    <div id="content-wrapper" class="d-flex flex-column">

      <div id="content">

        <Header></Header>
        
        <router-view></router-view>
      </div>

      <Footer></Footer>

    </div>
  </div>
  
</body>
</html>

</template>

<script>
import Sidebar from './Sidebar.vue';
import Header from './Header.vue';
import Index from './Index.vue';
import Footer from './Footer.vue';

export default {
    name: "Admin",
    components: {
        'Sidebar': Sidebar,
        'Header' : Header,
        'Index' : Index,
        'Footer' : Footer
    }
}
</script>