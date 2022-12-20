<template>
    <div id="main-banner">
        <h1>Fare la pizza</h1>
    </div>
</template>

<script>
export default {
 
}
</script>

<style scoped>
    #main-banner{
        background-image: url('/home/roberto/vscode_workspace/farelapizza/public/img/pizza.jpg');
        background-position: 0 -255px;
        background-size: cover;
        height: 500px;
        display: flex;
        align-items: center;
        justify-content: flex-start;
    }
    #main-banner h1{
        color:#a8a8a8;
        text-align: center;
        font-size: 60px;
        background-color: #222;
        padding: 20px 40px;
        
    }
</style>
