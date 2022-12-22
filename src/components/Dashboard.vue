<template>
    <div id="pizza-table">
        <Message :mensagem="msg" v-show="msg"/>
        <div>
            <div id="pizza-table-head">
                <div class="order-id">#:</div>
                <div>Cliente:</div>
                <div>Massa:</div>
                <div>Borda:</div>
                <div>Opcionais:</div>
                <div>Ações</div>
            </div>
        </div>
        <div id="pizza-table-rows">
            <div class="pizza-table-row" v-for="pizza in pizzas" :key="pizza.id" >
                <div class="order-number">{{pizza.id}}</div>
                <div>{{pizza.name}}</div>
                <div>{{pizza.massa}}</div>
                <div>{{pizza.borda}}</div>
                <div>
                    <ul>
                        <li v-for="(opcional, index) in pizza.opcionais" :key="index">{{opcional}}</li>
                    </ul>
                </div>
                <div>
                    <select name="status" class="status" @change="updatePizza($event, pizza.id)" >
                        <option v-for="sts in status" :key="sts.id" :value="sts.tipo" :selected="pizza.status==sts.tipo" >
                            {{sts.tipo}}
                        </option>
                    </select>
                    <button class="delete-btn" @click="deletePizza(pizza.id)">Cancelar</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import Message from "./Message.vue"
    
    export default{
        name:"Dashboard",
        components:{
            Message
        },

        data(){
            return{
                pizzas: null,
                id: null,
                status: [],
                msg:null
            }
        },
        methods:{
            async getPedidos(){
                const req = await fetch("http://localhost:3000/pizzas");
                const data =  await req.json();

                this.pizzas = data;

                this.getStatus();
            },
             
            async getStatus(){
                const req = await fetch("http://localhost:3000/status");
                const data =  await req.json();

                this.status = data;
            },

            async deletePizza(id){
                const req = await fetch(`http://localhost:3000/pizzas/${id}`,
                {method: "DELETE"});

                const res = await req.json();
                this.getPedidos();

                this.msg = `Pedido Nº ${id} foi removido`;
                 setTimeout(() => this.msg = "", 3000);
            },

            async updatePizza(event, pizzaId){

                const option = event.target.value;
                const json = JSON.stringify({ status: option });
                const req = await fetch(`http://localhost:3000/pizzas/${pizzaId}`,
                {method: "PATCH",
                 headers: {"content-type":"application/json"},
                 body: json});

                const res = await req.json();

                 this.msg = `Pedido Nº ${pizzaId} atualizado para: ${res.status}`;
                 setTimeout(() => this.msg = "", 3000);

            },


        },
        mounted(){
            this.getPedidos();
        }
    }
</script>
<style scoped>
    #pizza-table{
        max-width: 1200px;
        margin: 0 auto;
    }

    #pizza-table-head,
    #pizza-table-rows,
    .pizza-table-row{
        display:flex;
        flex-wrap: wrap;         
    }

    .status{
        font-size: 10px;
        font-weight: bold;
    }

    #pizza-table-head{
        font-weight: bold;
        padding: 12px;
        border-bottom: 3px solid #333;
    }

    #pizza-table-head div,
    .pizza-table-row div{
        width: 19%;
    }

    .pizza-table-row{
        width:100%;
        padding: 12px;
        border-bottom: 1px solid #ccc;
    }

    #pizza-table-head .order-id,
    .pizza-table-row .order-number{
        width: 5%;
    }

    select{
        padding: 12px 6px;
        margin-right: 12px;
    }

    .delete-btn{
        background-color: #222;
        color: #fcba03;
        font-weight: bold;
        border: 2px solid #222;
        padding: 10px;
        font-size: 16px;
        margin: 0 auto;
        cursor: pointer;
        transition: .5s;
    }

    .delete-btn:hover{
        background-color: transparent;
        color: #222;
    }

</style>
