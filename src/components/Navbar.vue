<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">

    <router-link class="navbar-brand" :to="{name : 'Home'}">
      <img width="100" alt="" src="../assets/icon.png" />
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
            Conta
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

        <!--
        <li class="nav-item">
          <router-link class="navlinks" :to="{name : 'Category'}">Categorias</router-link>
        </li> -->
      </ul>
    </div>
       <div class="navbar-brand">
      <div id="cart">
        <span id="nav-cart-count">{{cartCount}}</span>
        <router-link class="text-light" :to="{name : 'Cart'}"><i class="fa fa-shopping-cart"
            style="font-size:36px; color: #00453d;"></i></router-link>
      </div>
    </div>
  </nav>
    


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

  .bg-dark{
    background-color: black !important;
  }
*/
  .nav-link:hover{
    color: #00453d !important;
  }

  #nav-cart-count {
    background-color: pink;
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
    color: #00453d;
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
    background-color: #00453d;
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