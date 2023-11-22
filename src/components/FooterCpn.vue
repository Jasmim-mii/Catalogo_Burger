<template>
    <div id="footer">
        <p>Make Your Burger &copy;2022</p>
    </div>
</template>

<script>
export default {
    name: 'FooterCpn',
    components: {

    }

}
</script>

<style scoped>
#footer{
    background: #222;
    height: 5rem;
    border-top: 1rem solid #111;
    display: flex;
    align-items: center;
    justify-content: center;
    bottom: 0;
    width: 100%
}
#footer p {
    color: #fcb403;
    font-weight: 800;
}
</style>