<template>
  <BannerCpn />
  <div class="main-container">
     <h1>Monte o seu burguer:</h1>
     <BurgerForm />
  </div>
 
</template>

<script>
import BurgerForm from '@/components/BurgerForm.vue';
import BannerCpn from '../components/BannerCpn.vue'

export default {
  name: 'HomeView',
  components: {
    BannerCpn,
    BurgerForm
},
  data(){
    return{
      
    }

  }
}
</script>

<style scoped>

</style>
