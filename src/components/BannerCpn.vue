<template>
    <div id="main-burger">
        <h1 class="title">Make Your Burger</h1>
    </div>
</template>

<script>
export default {
   
    
}
</script>

<style scoped>
#main-burger{
    background-image: url('/public/img/hamburguerHome.jpeg');
    background-position: 0 -150px;
    background-size: cover;
    min-height: 30rem;
    display: flex;
    align-items: center;
    justify-content: flex-start
}
#main-burger .title{
    color: #f4f4f4;
    text-align: center;
    font-size: 3rem;
    background: #2222228c;
    padding: 2rem;
    border-radius: 0 4rem 4rem 0 ;
}

</style>