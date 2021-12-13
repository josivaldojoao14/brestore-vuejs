<template>
  <div class="container">
    <div class="row pt-5">

      <div class="div-img mr-5">
        <img :src="product.imageURL" :alt="product.name" class="img-fluid" />
      </div>
      <div class="col-md-6">
        <p class="category">Categoria: {{ category.categoryName }}</p>
        <h4 class="title">{{ product.name }}</h4>
        <h6 class="price">R$ {{ product.price }}</h6>
        <p class="description">
          Descrição: {{ product.description }}
        </p>

        <div class="d-flex flex-row justify-content-between botoes">

          <div>
            <button type="button" id="add-to-cart-button" class="btn" @click="addToCart(this.id)">
              <i class="bi bi-bag"></i>
              Adicionar ao carrinho
            </button>
          </div>

          <div>
            <button type="button" id="wishlist-bt" :class="{ product_added_wishlist: isAddedToWishlist }"
              @click="addToWishList(this.id)">
              <i class="bi bi-heart"></i>
              Favoritar
            </button>
          </div>
        </div>

        <div id="accordion">
          <div class="card">
            <div class="card-header" id="headingOne">
              <h5 class="mb-0">
                <button class="btn btn-link" data-toggle="collapse" data-target="#collapseOne" aria-expanded="false"
                  aria-controls="collapseOne">
                  <i class="bi bi-caret-down-fill"></i> Características
                </button>
              </h5>
            </div>

            <div id="collapseOne" class="collapse show" aria-labelledby="headingOne" data-parent="#accordion">
              <div class="card-body ml-3">
                <li>Lorem ipsum dolor sit amet</li>
                <li>Lorem ipsum dolor sit amet</li>
                <li>Lorem ipsum dolor sit amet</li>
                <li>Lorem ipsum dolor sit amet</li>
              </div>
            </div>
          </div>
        </div>

      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        product: {},
        category: {},
        id: null,
        token: null,
        isAddedToWishlist: false,
        wishlistString: "Adicionar à lista de desejos",
        quantity: 1,
      };
    },
    props: ["baseURL", "products", "categories"],
    methods: {
      addToWishList(productId) {
        if (!this.token) {
        swal({
          text: "Faça o login para realizar essa ação!",
          icon: "error",
        });
        return;
      }
        axios
          .post(`${this.baseURL}wishlist/add?token=${this.token}`, {
            id: productId,
          })
          .then(
            (response) => {
              if (response.status == 201) {
                this.isAddedToWishlist = true;
                this.wishlistString = "Adicionado à lista de desejos";
              }
            },
            (error) => {
              console.log(error);
            }
          );
      },
      addToCart(productId) {
        if (!this.token) {
        swal({
          text: "Faça o login para realizar essa ação!",
          icon: "error",
        });
        return;
        }
        axios
          .post(`${this.baseURL}cart/add?token=${this.token}`, {
            productId: productId,
            quantity: this.quantity,
          })
          .then(
            (response) => {
              if (response.status == 201) {
                // refresh nav bar
                this.$emit("fetchData");
                this.$router.replace("/cart");
              }
            },
            (error) => {
              console.log(error);
            }
          );
      },

      listCartItems() {
        axios.get(`${this.baseURL}cart/?token=${this.token}`).then(
          (response) => {
            if (response.status === 200) {
              this.$router.push("/cart");
            }
          },
          (error) => {
            console.log(error);
          }
        );
      },
    },
    mounted() {
      this.id = this.$route.params.id;
      this.product = this.products.find((product) => product.id == this.id);
      this.category = this.categories.find(
        (category) => category.id == this.product.categoryId
      );
      this.token = localStorage.getItem("token");
    },
  };
</script>

<style>
  * {
    font-family: 'Poppins', sans-serif;
  }

  .title {
    font-size: 30px;
    font-weight: bold;
  }

  .price {
    font-size: 32px;
  }

  .category {
    font-weight: 400;
  }

  .div-img {
    align-self: center;
  }

  .img-fluid {
    width: 400px;
    height: 400px;
    border-radius: 10px;
    align-self: center;
  }

  /* Chrome, Safari, Edge, Opera */
  input::-webkit-outer-spin-button,
  input::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
  }

  .btn-link{
    color: black;
    font-family: 'Poppins', sans-serif;
    text-decoration: none !important;
  }

  /* Firefox */
  input[type="number"] {
    -moz-appearance: textfield;
  }

  #add-to-cart-button {
    height: 45px;
    padding-left: 45px;
    padding-right: 45px;
    border-radius: 0;
    color: white;
    font-family: 'Poppins';
    font-weight: bold;
    margin-bottom: 20px;
    letter-spacing: 1px;
    background-color: #00453d;
  }

  #add-to-cart-button:hover {
    background-color: rgb(3, 93, 84);
  }

  #wishlist-bt {
    height: 45px;
    padding-left: 45px;
    padding-right: 45px;
    border-radius: 0;
    color: white;
    font-family: 'Poppins';
    font-weight: bold;
    margin-bottom: 20px;
    letter-spacing: 1px;
    background-color: #cc3c57;
    cursor: pointer;
    border: none;
  }

  #wishlist-bt:hover {
    background-color: #f32047;
  }

  @media (max-width: 576px){
    .row{
      padding-top: 15px !important;
    }

    .botoes{
      display: block !important;
    }

    .div-img{
      margin-right: 0 !important;
    }

    .img-fluid{
      height: 350px;
      width: 350px;
      padding: 10px;
      margin-left: 5px;
    }

    .category{
      display: none;
    }

    .title{
      margin-top: 15px;
      font-size: 21px;
    }

    .price{
      font-size: 23px;
    }

    .description{
      font-size: 14px;
    }
  }
</style>