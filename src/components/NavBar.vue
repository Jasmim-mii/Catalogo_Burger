<template>
    <nav id="navbar">
        <router-link to="/"><img id="" :src="logo" :alt="alt"></router-link>
        <div class="menu">
            <router-link to="/">Home</router-link> 
            <router-link to="/checkin">Pedidos</router-link> 
            <router-link to="/contact">Contact</router-link> 
        </div>
    </nav>
</template>

<script>
export default {
    name: 'NavBar',
    props: ["logo", "alt"]
    
}
</script>

<style scoped>
#navbar{
    background: #222;
    border-bottom: .4rem solid #111;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding-top: 1rem;
    padding-bottom: 1rem
}
#navbar .menu a{
    margin: .8rem;
    transition: .5s
}
#navbar .menu a:hover{
    color: #fff
}

</style>