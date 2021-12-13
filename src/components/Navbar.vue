<template>
<!--
  <nav class="navbar navbar-expand-lg navbar-light">

    <router-link class="navbar-brand" :to="{name : 'Home'}">
      <img width="100" alt="" src="../assets/icon-branco.png" />
    </router-link>

    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#collapsibleNavbar">
      <i class="bi bi-list fa-lg icon-menu"></i>
    </button>

    <div class="collapse navbar-collapse" id="collapsibleNavbar" style="align-self: center;">

      <ul class="navbar-nav mr-auto mt-2 mt-lg-0">

        <li class="nav-item">
          <router-link class="nav-link" :to="{name : 'Home'}">Início</router-link>
        </li>

        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown"
            aria-haspopup="true" aria-expanded="false">
            <i class="bi bi-person-circle" style="font-size:36px;" ></i>
          </a>
          <div class="dropdown-menu" aria-labelledby="navbarDropdown">
            <router-link class="dropdown-item" v-if="!token" :to="{name: 'Signin'}">Entrar</router-link>
            <router-link class="dropdown-item" v-else :to="{name : 'Wishlist'}">Lista de desejos</router-link>
            <router-link class="dropdown-item" v-if="!token" :to="{name: 'Signup'}">Cadastrar</router-link>
            <router-link class="dropdown-item" :to="{name : 'Order'}">Pedidos</router-link>
            <a class="dropdown-item" v-if="token" href="#" @click="signout">Sair</a>
          </div>
        </li>

        <li class="nav-item">
          <router-link class="nav-link" :to="{name: 'Admin'}">Adicione um produto</router-link>
        </li>


        <li class="nav-item">
          <router-link class="navlinks" :to="{name : 'Category'}">Categorias</router-link>
        </li>
 
      </ul>
    </div>
       <div class="navbar-brand">
      <div id="cart">
        <span id="nav-cart-count">{{cartCount}}</span>
        <router-link class="text-light" :to="{name : 'Cart'}"><i class="fa fa-shopping-cart"
            style="font-size:36px; color: white;"></i></router-link>
      </div>
    </div>
  </nav>
  -->
    <!-- Navbar -->
<nav class="navbar navbar-expand-md navbar-light">

  <router-link class="navbar-brand" :to="{name : 'Home'}">
    <img src="../assets/icon-branco.png" height="30" alt="mdb logo">
  </router-link>

  <!-- Collapse button -->
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#basicExampleNav1"
    aria-controls="basicExampleNav1" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>

  <!-- Links -->
  <div class="collapse navbar-collapse" id="basicExampleNav1">

    <!-- Right -->
    <ul class="navbar-nav ml-auto" style="align-items: center; cursor: pointer;">
      <li class="nav-item">
        <router-link class="nav-link item-hov" :to="{name : 'Home'}">Início</router-link>
      </li>
      <li class="nav-item">
        <router-link class="nav-link item-hov" v-if="!token" :to="{name: 'Signin'}">Adicione um produto</router-link>
        <router-link class="nav-link item-hov" v-else-if="token" :to="{name: 'AddProduct'}">Adicione um produto</router-link>
        
      </li>
      <li class="nav-item dropdown">
        <a class="nav-link dropdown-toggle waves-effect" id="navbarDropdownMenuLink3" data-toggle="dropdown"
          aria-haspopup="true" aria-expanded="true">
          <i class="fa bi-person-circle" style="font-size:30px;"></i>
        </a>
        <div class="dropdown-menu dropdown-menu-right" aria-labelledby="navbarDropdownMenuLink">
          <router-link class="dropdown-item" v-if="!token" :to="{name: 'Signin'}">Entrar</router-link>
            <router-link class="dropdown-item" v-else :to="{name : 'Wishlist'}">Lista de desejos</router-link>
            <router-link class="dropdown-item" v-if="!token" :to="{name: 'Signup'}">Cadastrar</router-link>
            <router-link class="dropdown-item" v-if="!token" :to="{name: 'Signin'}">Pedidos</router-link>
            <router-link class="dropdown-item" v-if="token" :to="{name: 'Order'}">Pedidos</router-link>
            <a class="dropdown-item" v-if="token" href="#" @click="signout">Sair</a>
        </div>
      </li>

      <div id="nav-item">
        <span id="nav-cart-count">{{cartCount}}</span>
        <router-link class="text-light" v-if="token" :to="{name : 'Cart'}"><i class="fa fa-shopping-cart"
          style="font-size:36px; color: white;"></i>
        </router-link>

        <router-link class="text-light" v-if="!token" :to="{name: 'Signin'}"><i class="fa fa-shopping-cart"
          style="font-size:36px; color: white;"></i>
        </router-link>
      </div>

      
    </ul>

  </div>
  <!-- Links -->

</nav>
<!-- Navbar -->


</template>

<script>
  export default {
    name: "Navbar",
    props: ["cartCount"],
    data() {
      return {
        token: null
      }
    },
    methods: {
      signout() {
        localStorage.removeItem('token');
        this.token = null;
        this.$router.push({
          name: 'Home'
        });
        swal({
          text: "Você saiu com sucesso.",
          icon: "success",
          closeOnClickOutside: false,
        });
      }
    },
    mounted() {
      this.token = localStorage.getItem('token');
    }
  }
</script>

<style scoped>
  /*
  .navlinks {
    color: #00453d;
    margin-right: 20px;
  }

  .nav-link {
    color: rgba(255,255,255);
  }
*/
  .navbar{
    background-color: #00453d !important;
  }

  .nav-item{
    margin-left: 5px;
    margin-right: 5px;
  }

  .nav-link:hover{
    color: white !important;
  }

  #nav-cart-count {
    background-color: #cc3c57;
    color: white;
    border-radius: 50%;
    position: absolute;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 15px;
    height: 15px;
    font-size: 12px;
    margin-left: 22px;
    padding: 5px;
  }
  #cart {
    color: white;
  }

  .navbar-light .navbar-nav .nav-link {
    color: white;
  }

  .item-hov:hover {
    color: #cc3c57 !important;
  }
  

  .form-control{
    border-radius: 20px;
    padding: 15px;
  }

  .input-group-text{
    border-bottom-right-radius: 20px !important;
    border-top-right-radius: 20px !important;
  }

  li{
    padding-bottom: 0;
  }

  .navbar-toggler{
    background-color: white;
  }

  .icon-menu{
    color: white;
  }

  @media (max-width: 576px){
    .navbar-brand{
      text-align: center;
    }
  }
  
</style>