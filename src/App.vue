<template>
  <Navbar :cartCount="cartCount"  v-if="!['Signup', 'Signin'].includes($route.name)"/>
  <div style="min-height: 60vh">
  <router-view v-if="products && categories"
    :baseURL="baseURL"
    :products="products"
    :categories="categories"
    @fetchData = "fetchData">
  </router-view>
  </div>
  <Footer v-if="!['Signup', 'Signin'].includes($route.name)"/>
</template>

<script>
import Navbar from "./components/Navbar.vue"
import Footer from "./components/Footer.vue"
import axios from 'axios'
export default {
  data() {
    return {
      baseURL : "https://brestoreapi.herokuapp.com/",
      baseURL2 : "https://gabrielidsm-fretecorreios.herokuapp.com/",
      products : null,
      categories : null,
      frete: null,
      key : 0,
      token: null,
      cartCount: 0
    }
  },

  components : {Footer, Navbar},
  methods : {
    async fetchData() {
      await axios.get(this.baseURL + "product/")
      .then(res => this.products = res.data)
      .catch(err => console.log(err))

      await axios.get(this.baseURL + "category/")
      .then(res => this.categories = res.data)
      .catch(err => console.log(err))

      axios.defaults.headers.get['Access-Control-Allow-Origin'] = '*';
      axios.defaults.headers.post['Access-Control-Allow-Origin'] = '*';

      if(this.token) {
        await axios.get(`${this.baseURL}cart/?token=${this.token}`).then((response) => {
          if(response.status==200){
            this.cartCount = Object.keys(response.data.cartItems).length
          }
        },
        (error)=>{
          console.log(error)
        });
      }
    },
  },
  mounted() {
    this.token = localStorage.getItem("token");
    this.fetchData();
  }
}
</script>

<style>
html{
  overflow-y: scroll;
}
</style>
