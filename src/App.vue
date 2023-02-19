<template>
  <NavBar :logo="logo_src" :alt="app_name"/>
  <RouterView />
  <Footer />
</template>

<script>
  import NavBar from './components/Navbar.vue'
  import Footer from './components/Footer.vue'

  export default {
    components :{
      NavBar,
      Footer
    },
    data(){
      return{
        logo_src:"/img/logo.png",
        app_name: "Contact List"
      }
    }
  }
</script>

<style >
  *{
    font-family: Helvetica;
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }
  .main-container{
    margin: 50px;
    min-height: 80vh;
  }
  h1{
    text-align: center;
    font-size: 42px;
    margin-bottom: 30px;
    color: #222;
  }
</style>
