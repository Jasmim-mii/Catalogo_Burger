<template>
    <div class="message-container"><p>{{ msg }}</p></div>
</template>
<script>
export default {
    name:"MessageForm",
    props: {
        msg: String
    }
}
</script>
<style scoped>
.message-container{
    background-color: #cce5ff;
    border-radius: 0.5rem;
    padding: .8rem;
    margin-bottom: 2rem ;
}
.message-container p {
    color: #004085;
    text-align: center;
    font-weight: 500;
}
</style>