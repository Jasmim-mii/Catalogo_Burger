<template>
  <NavBar :logo="logoSrc" :alt="altDescrip" />
  <router-view/>
  <footer-cpn />
</template>

<script>
import NavBar from './components/NavBar.vue'
import FooterCpn from './components/FooterCpn.vue';

export default {
  name: 'App',
  components: {
    NavBar,
    FooterCpn
  },
  data(){
    return{
      logoSrc: "/img/logo.png",
      altDescrip: "Make Your Burger"
    }
  }
}
</script>

<style>
*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: Helvetica;
}
nav{
  padding: 0 3rem;
}
.main-container{
  padding: 0 3rem;
  background: #e9e8e8;
  min-height: 27rem;
}
a {
  text-decoration: none;
  color: #b9b9b9;
  letter-spacing: .1rem;
}
h1{
  text-align: center;
  color: #101010;
  font-weight: 800;
  letter-spacing: .1rem;
  padding: 1.8rem 0;
}
p{
  font-size: 1rem;
  color: #222222;
  letter-spacing: .1rem;
}

</style>
