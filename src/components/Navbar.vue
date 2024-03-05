<template>
  <nav id="nav">
    <router-link to="/" id="logo-url">
        <img :src="logo" :alt="alt" id="logo">
    </router-link>
    <router-link id="sub-tittle" to="/">HOME</router-link> 
    <router-link id="sub-tittle" to="/pedidos">PEDIDOS</router-link>
  </nav>
</template>

<script>
export default {
  name: "Navbar",
  props: ["logo", "alt"]
};
</script>

<style scoped>
  #nav {
    background-color: #222;
    border-bottom: 4px solid #111;
    padding: 15px 50px;
    display: flex;
    justify-content:flex-end ;
    align-content: center;
  }
  #nav #logo-url{
    margin: auto;
    margin-left: 0;
  }

  #logo{
    width: 50px;
    height: 50px;
  }
  #nav a{
    color: #FCBA03;
    text-decoration: none;
    margin: 17px;
    transition: .5s;
  }

  #nav a:hover{
    color: #FFF;
  }
  


</style>
