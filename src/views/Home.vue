<template>
  <div id="home">
    <div id="start-shopping" class="container">
      <div class="row">
        <div class="col-12 text-center">
          <h2 class="pt-5 titulo-grande">Categorias em destaque</h2>
        </div>
      </div>
      <div class="row">
        <div v-for="index in this.category_size" :key="index" class="col-md-6 col-xl-3 col-12 pt-3  justify-content-around d-flex grid-categoria">
          <CategoryBox :category="categories[index-1]">
          </CategoryBox>
        </div>
      </div>
    </div>

    <div class="container">
      <div class="row">
        <div class="col-12 text-center">
          <h2 class="pt-5 titulo-grande">Produtos adicionados recentemente</h2>
        </div>
      </div>
      <div class="row">
        <div v-for="index in this.product_size" :key="index" class="col-md-6 col-xl-3 col-12 pt-3  justify-content-around d-flex grid-produto">
          <ProductBox :product="products[index-1]">
          </ProductBox>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import ProductBox from "../components/Product/ProductBox";
  import CategoryBox from "../components/Category/CategoryBox";
  export default {
    name: 'Home',
    components : { ProductBox, CategoryBox},
    props : ["baseURL", "products", "categories"],
    data(){
      return{
        category_size:0,
        product_size:0
      }
    },
    mounted(){
      this.category_size = this.categories.length;
      this.category_size = Math.min(6, this.category_size);

      this.product_size = this.products.length;
      this.product_size = Math.min(8, this.product_size);
    }
  }
</script>

<style>
  .page-holder {
    min-height: 30vh;
  }

  .bg-cover {
    background-size: cover !important;
    background-position: center center !important;
  }

  #background-div {
    background: url(../assets/home.png)
  }

  #heading {
    text-decoration: none;
    font-family: 'Roboto', sans-serif;
    font-weight: 400;
    opacity: 0.8;
    font-family: 'Josefin Sans', sans-serif;
  }

  #content {
    opacity: 0.8;
  }

  h2 {
    font-family: 'Josefin Sans', sans-serif;
  }

  
@media (max-width: 576px){
  .row{
    display: inline-flex !important;
  }

  .grid-categoria{
  max-width: 50%;
  }

  .card-title{
  font-size: 15px;
  margin-bottom: 0 !important;
  }

  .titulo-grande{
    font-size: 24px;
        margin-left: 30px;
    margin-right: 30px;
  }

  .grid-produto{
  max-width: 50%;
  }
}

  
</style>
