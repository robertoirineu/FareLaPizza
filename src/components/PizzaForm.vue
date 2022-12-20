<template>
    <div>
        <p>Componente de mensagem</p>
        <div>
            <form id="pizza-form" >
                <div class="input-container">
                    <label for="name">Nome do cliente: </label>
                    <input type="text" id="name" name="name" v-model="name" placeholder="Digite o seu nome" />
                </div>
              
                <div class="input-container">
                    <label for="borda">Escolha a borda:</label>
                    <select name="borda" id="borda" v-model="borda">
                        <option value="">Selecione o tipo de borda</option>
                        <option value="SemBorda">Sem borda</option>
                    </select>
                </div>
              
                <div class="input-container">
                    <label for="massa">Escolha a massa:</label>
                    <select name="massa" id="massa" v-model="pao">
                        <option value="">Escolha o tipo de massa</option>
                        <option value="Fina">Fina</option>
                    </select>
                </div>
                
                <div id="opcionais-container" class="input-container">
                    <label for="opcionais" id="opcionais-title">Selecione os opcionais:</label>
                    <div class="check-box-container">
                        <input type="checkbox" id="opcionais" name="opcionais" v-model="opcionais" value="Salame"/>
                        <span>Calabresa</span>
                    </div>
                    <div class="check-box-container">
                        <input type="checkbox" id="opcionais" name="opcionais" v-model="opcionais" value="Salame"/>
                        <span>Oregano</span>
                    </div>
                    <div class="check-box-container">
                        <input type="checkbox" id="opcionais" name="opcionais" v-model="opcionais" value="Salame"/>
                        <span>Cebola</span>
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
    export default{
    name:"PizzaForm",

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