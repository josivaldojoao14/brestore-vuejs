<template>
  <nav class="navbar navbar-expand-lg">

    <router-link class="navbar-brand" style="margin-right: 0px;" :to="{name : 'Home'}">
      <img width="100" alt="" class="d-inline-block align-middle mr-2" src="../assets/icon.png" />
    </router-link>


    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent"
     aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>

    <div class="collapse navbar-collapse" id="navbarSupportedContent" style="align-items: center;">

      <!--
      <form class="form-inline ml-auto mr-auto">
        <div class="input-group">
          <input size="100" type="text" class="form-control" placeholder="Procure por algum produto" aria-label="Username" aria-describedby="basic-addon1">
          <div class="input-group-prepend">
            <span class="input-group-text" id="search-button-navbar">
              <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" fill="pink" class="bi bi-search" viewBox="0 0 16 16">
                <path d="M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0z"/>
              </svg>
            </span>
          </div>
        </div>
      </form>
      -->


      <ul class="navbar-nav ml-auto" style="align-items: center;">

        <li class="nav-item">
          <router-link class="navlinks" :to="{name : 'Home'}" >Início</router-link>
        </li>

        <li class="nav-item dropdown">
          <a class="navlinks dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
            Conta
          </a>
          <div class="dropdown-menu" aria-labelledby="navbarDropdown">
            <router-link class="dropdown-item" v-if="!token" :to="{name: 'Signin'}">Entrar</router-link>
            <router-link class="dropdown-item" v-else :to="{name : 'Wishlist'}" >Lista de desejos</router-link>
            <router-link class="dropdown-item" v-if="!token" :to="{name: 'Signup'}">Cadastrar</router-link>
            <router-link class="dropdown-item"  :to="{name : 'Order'}">Pedidos</router-link>
            <router-link class="dropdown-item"  :to="{name: 'Admin'}">Adicione um produto</router-link>
            <a class="dropdown-item" v-if="token" href="#" @click="signout">Sair</a>
          </div>
        </li>

        <li class="nav-item">
          <router-link class="navlinks" :to="{name : 'Product'}">Produtos</router-link>
        </li>

        <li class="nav-item">
          <router-link class="navlinks" :to="{name : 'Category'}">Categorias</router-link>
        </li>

        <li class="nav-item">
          <div id="cart">
            <span id="nav-cart-count">{{cartCount}}</span>
            <router-link class="text-light" :to="{name : 'Cart'}"><i class="fa fa-shopping-cart" style="font-size:36px; color: #00453d;"></i></router-link>
          </div>
        </li>
      </ul>
    </div>
  </nav>

  
</template>

<script>
export default {
  name : "Navbar",
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
      this.$router.push({name:'Home'});
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

  #search-button-navbar {
    background-color: #00453d;
    border-color: #bbbaba;
    border-top-right-radius: 2px;
    border-bottom-right-radius: 2px;
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
    font-size: 15px;
    margin-left: 22px;
    padding: 5px;
  }
  #cart {
    position: relative;
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

</style>
