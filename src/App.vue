<template>
  <Navbar @fazer-login="fazerLogin" :logado="!logado"/>
  <LoginVue @fazer-login="fazerLogin" v-if="logado"/>
  <router-view v-show="!logado"/>
  <Footer />
</template>

<script>

  import Navbar from './components/Navbar.vue';
  import Footer from './components/Footer.vue';
  import LoginVue from './views/Login.vue';

  export default{
    components:{
      Navbar,
      Footer,
      LoginVue
      },
      methods:{
        fazerLogin(){
          console.log(this.logado);
          this.logado = !this.logado
        }
      },
      data(){
        return {
          logado: Boolean
        }
      }
  }
</script>

<style>
  *{
    font-family: Helvetica;
    padding: 0 auto;
    margin: 0 auto;
    box-sizing: border-box;
  }

  .main-container{
    margin: 50px;
    min-height: 1px;
  }

  h1{
    text-align: center;
    font-size: 42px;
    margin-bottom: 30px;
    color: #222;
  }
</style>