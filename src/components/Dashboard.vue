<template>
    <div id="table" >
    <Message :msg="msg" v-show="msg"/>
    <div>
      <div id="table-heading">
        
      </div>
    </div>
    <div id="table-rows">
      <div class="table-row" v-for="contact in contacts" :key="contact.id">
        <div class="order-number">{{ contact.id }}</div>
            <div> Name: {{ contact.nome }}</div>
            <div>Phone: {{ contact.phone }}</div>
            <div>E-mail: {{ contact.email }}</div>  
            <div>
              <button class="delete-btn" @click="deleteContact(contact.id)">Delete</button></div>    
            </div>
    </div>
  </div>
</template>
<script>
import Message from './Message.vue'
export default {
    name: "Dashboard",
    data(){
        return{
          contacts: null,
          contacts_id: null,
          status: [],
          msg: null
        }
    },
    methods:{
        async routeResolv(){
          return `/DetailsView/${e.target.id}`
        },
        async getCaontacts(){

            const req = await fetch("http://localhost:3000/contact")
            const data = await req.json()

            this.contacts = data
        
            this.getStatus()
        },
        async getStatus(){
            const req = await fetch("http://localhost:3000/options")
            const data = await req.json()

            this.status = data
        },
        async deleteContact(id){
            const req = await fetch(`http://localhost:3000/contact/${id}`, {
                method: "DELETE"
            })
            const res = await req.json()
            //colocar msg no sistema
            this.msg =`Pedido removido com sucesso!`

            //Limpar mensagem
            setTimeout(()=>this.msg = "" ,3000)
            this.getCaontacts()
        },        
    },
    mounted(){
        this.getCaontacts()
    },
    components: {
    Message,
}
}
</script>
<style scoped>
    #table {
    max-width: 1200px;
    margin: 0 auto;
  }
  #table-heading,
  #table-rows,
  .table-row {
    display: flex;
    flex-wrap: wrap;
    flex-direction: column;
  }
  #table-heading {
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
  }
  .table-row {
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #CCC;
  }
  #table-heading div,
  .table-row div {
    width: 19%;
  }
  #table-heading .order-id,
  .table-row .order-number {
    width: 5%;
  }
  select {
    padding: 12px 6px;
    margin-right: 12px;
  }
  .delete-btn {
    background-color: #222;
    color:#fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
    margin-right: 10px;
    margin-top: 10px;
  }
  
  .delete-btn:hover {
    background-color: transparent;
    color: #222;
    
  }
</style>