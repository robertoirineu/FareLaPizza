<template>
    <div>
        <Message :mensagem="msg" v-show="msg"/>
        <div>
            <form id="pizza-form" @submit="createPizza($event)">
                <div class="input-container">
                    <label for="name">Nome do cliente: </label>
                    <input type="text" id="name" name="name" v-model="name" placeholder="Digite o seu nome" />
                </div>
              
                <div class="input-container">
                    <label for="borda">Escolha a borda:</label>
                    <select name="borda" id="borda" v-model="borda">
                        <option v-for="borda in bordas" :key="borda.id" :value="borda.tipo">
                            {{borda.tipo}}
                        </option>
                    </select>
                </div>
              
                <div class="input-container">
                    <label for="massa">Escolha a massa:</label>
                    <select name="massa" id="massa" v-model="massa">
                        <option v-for="massa in massas" :key="massa.id" :value="massa.tipo">
                            {{massa.tipo}}
                        </option>
                    </select>
                </div>
                
                <div id="opcionais-container" class="input-container">
                    <label for="opcionais" id="opcionais-title">Selecione os opcionais:</label>
                    <div class="check-box-container" v-for="option in opcionaisdata" :key="option.id">
                        <input type="checkbox" id="opcionais" name="opcionais" v-model="opcionais" :value="option.tipo"/>
                        <span>{{option.tipo}}</span>
                    </div>                    
                </div>
                <div class="input-container">
                    <input type="submit" class="submit-btn" value="Criar minha pizza" /> 
                </div>
                
            </form>
        </div>
    </div>
</template>

<script>
    import Message from "./Message.vue"

    export default{
        components:{
            Message
        }, 

        name:"PizzaForm",
        data(){
            return{
                massas: null,
                bordas: null,
                opcionaisdata: null,
                name: null,
                massa: null,
                borda: null,
                opcionais: [],
                msg: null
            }
        },

        methods:{
            async getIngredintes(){
                const req = await fetch('http://localhost:3000/ingredientes');
                const data = await req.json();

                this.massas = data.massas;
                this.bordas = data.bordas;
                this.opcionaisdata = data.opcionais;
            },

            async createPizza(e){
                e.preventDefault();
                const data = {
                    name: this.name,
                    massa: this.massa,
                    borda: this.borda,
                    opcionais: Array.from(this.opcionais),
                    status: "Solicitado"
                };

                const dataJson = JSON.stringify(data);

                const req = await fetch("http://localhost:3000/pizzas",{
                    method:"POST",
                    headers: {"Content-type":"application/json"},
                    body: dataJson
                });

                const res = await req.json();

                this.msg = `Pedido Nº ${res.id} realizado! ;) `;

                setTimeout(() => this.msg = "", 3000);
                this.name = ""
                this.massa = ""
                this.borda = ""
                this.opcionais = [],
                this.status = ""

            }
        },

        mounted(){
            this.getIngredintes();
        }
}

</script>

<style scoped>
    #pizza-form{
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
        border-left: 4px solid #fcba03;
    }

    input, select{
        padding: 5px 10px;
        width: 300px;
    }

    #opcionais-container{
        flex-direction: row;
        flex-wrap: wrap;
    }

    #opcionais-title{
        width:100%;        
    }
    .check-box-container{
        display: flex;
        align-items: flex-start;
        width: 50%;
        margin-bottom: 20px; 
    }
    .check-box-container span,
    .check-box-container input{
        width: auto;
    }
    
    .check-box-container span{
        margin-left: 6px;
        font-weight: bold;
    }

    .submit-btn{
        background-color: #222;
        color: #fcba03;
        font-weight: bold;
        border: 2px solid;
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