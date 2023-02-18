<template lang="">
    <div>
        <p>Componente de mensagem</p>
    </div>
    <div>
        <form id="burger-form">
            <div class="input-container">
                <label for="name">Customer Name: </label>
                <input type="text" name="name" id="name" v-model="name" placeholder="Write your name">
            </div>
            <div class="input-container">
                <label for="bread">Select your bread:</label>
                <select name="bread" id="bread" v-model="bread">
                <option value="">Selecione o seu pão</option>
                <option v-for="bread in breads" :key="bread.id" :value="bread.tipo">{{ bread.tipo }}</option>
                </select>
            </div>
            <div class="input-container">
                <label for="name">Select your meat:</label>
                <select name="meat" id="meat" v-model="meat">
                    <option value="">Select your meat</option>
                    <option v-for="meat in meats" :key="meat.id" :value="meat.tipo">{{ meat.tipo }}</option>
                </select>
            </div>
            <div id="options-container" class="input-container">
                <label for="options" id="options-title">Select your options:</label>
                <div class="checkbox-container" v-for="opcional in opcionaisdata" ::key="opcional.id">
                    <input type="checkbox" name="options" v-model="options" :value="opcional.tipo">
                    <span>{{opcional.tipo}}</span>
                </div>                
            </div>
            <div class="input-container">
                <input type="submit" value="Make my burger" class="submit-btn">                
            </div>
        </form>
    </div>
</template>
<script>
export default {
    name: "BurgerForm",
    data(){
        return{
            breads: null,
            meats: null,
            opcionaisdata: null,
            nome: null,
            bread: null,
            meat: null,
            opcionais: [],
            status: "Solicitado",
            msg: null
        }
    },
    methods: {
        async getIngredients(){
            const req = await fetch('http://localhost:3000/ingredientes')
            const data = await req.json()
            this.breads = data.paes
            this.meats = data.carnes
            this.opcionaisdata = data.opcionais
        }
    },
    mounted(){
        this.getIngredients()
    }
}
</script>
<style scoped>
    #burger-form{
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