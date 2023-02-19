<template lang="">
    <div>
        <Message :msg="msg" v-show="msg"/>
    </div>
    <div>
        <form id="form" @submit="createContact">
          <div class="input-container">
              <label for="nome">Name: </label>
              <input type="text" nome="nome" id="nome" v-model="nome" placeholder="Write your name"  minlength="5">
          </div>
          <div class="input-container">
              <label for="phone">Contact: </label>
              <input type="tel" id="phone" name="phone" v-model="phone" placeholder="Write your phone" minlength="9">
          </div>
          <div class="input-container">
              <label for="email">Email: </label>
              <input type="email" id="email" name="email" v-model="email" placeholder="Write your email">
          </div>
          <div class="input-container">
              
              <form>
                <label for="picture">Select your picture:</label>
                <input type="file" id="picture" name="picture" accept="image/*">
              </form>
          </div>
        
          <div class="input-container">
              <input type="submit" value="Salve contact" class="submit-btn">                
          </div>
      </form>
    </div>
</template>
<script>
import Message from './Message.vue'
export default {
    name: "ContactForm",
    data(){
        return{
            nome: null,
            phone: null,
            email: null,
            picture: null,
            msg: null
        }
    },
    methods: {
        async createContact(e){  
            e.preventDefault();        
          const data = {
              nome: this.nome,
              phone: this.phone, 
              email: this.email,
              picture: this.picture
          }
          const dataJson = JSON.stringify(data)          
          const req = await fetch("http://localhost:3000/contact", {
              method: "POST",
              headers: {"Content-Type": "application/json"},
              body: dataJson
          })          
          const res = await req.json()
          //colocar msg no sistema
          this.msg =`Contact Nº${res.id} salved!`

          //Limpar mensagem
          setTimeout(()=>this.msg = "" ,3000)        
          

          //limpar os campos
          this.nome = ""
          this.phone = ""
          this.email = ""
          this.picture = ""
          
      },    
    },
    
    components: {
        Message
    }
}
</script>
<style scoped>
    #form{
        max-width: 400px;
        margin: 0 auto;
    }
    .input-container{
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
    }
    label{
        font-weight: bold;
        margin-bottom: 15px;
        color: #222;
        padding: 5px 10px;
        border-left: 4px solid #FCBA03;
    }
    input, select{
        padding: 5px 10px;
        width: 300px;
    }
    #options-container{
        flex-direction: row;
        flex-wrap: wrap;
    }
    #options-title{
        width: 100%;
    }
    .checkbox-container{
        display: flex;
        align-items: center;
        width: 50%;
        margin-bottom: 20px;
    }
    .checkbox-container span,
    .checkbox-container input{
        width: auto;
    }
    .checkbox-container span{
        margin-left: 6px;
        font-weight: bold;
    }
    .submit-btn{
        background-color: #222;
        color: #FCBA03;
        font-weight: bold;
        border: 2px solid #222;
        padding: 10px;
        font-size: 16px;
        margin: 0 auto;
        cursor: pointer;
        transition: .5s;
    }
    .submit-btn:hover{
        background-color: transparent;
        color: #222;
    }
</style>