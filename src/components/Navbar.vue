<template>
    <nav id="nav" >
        
        <router-link to="/" id="logo-url">
            <img :src="logo" :alt="alt" id="logo" />
        </router-link>

        <router-link to="/">Home</router-link> 
        <router-link to="/Pedidos">Pedidos</router-link>
    </nav>
</template>
<script>
    export default{
        name:"navbar",
        props:["logo", "alt"]
    }

</script>
<style scoped>

#nav{
    background-color: #171717;
    border-bottom: 4px;
    padding: 15px 50px;
    display: flex;
    justify-content: flex-end;
    align-items: center;
}

#nav #logo-url{
    margin: auto;
    margin-left: 0px;
}

#logo{
    width: 40px;
    height: 40px;
}

#nav a{
    color: #fc0339;
    text-decoration: none;
    margin: 12px;
    transition: .5s;
    font-weight: bolder;
}

#nav a:hover{
    color: #fff;
}
</style>