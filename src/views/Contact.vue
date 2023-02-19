<template>
  <main class="main-container">    
   <h1>Add your contact: </h1>
   <ContactForm/>
  </main>
</template>
<script>
  import ContactForm from "../components/ContactForm.vue"
  export default {
    name: "Home",
    components: {
      ContactForm
    }
  }
</script>