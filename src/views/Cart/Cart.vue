<template>
  <div class="container">
    <div class="row">
      <div class="col-12 text-center mb-2">
        <h4 class="pt-3">Carrinho</h4>
      </div>
    </div>

    <div v-if="len === 0" :to="{name : 'Home'}" class="row mt-1  pt-3 justify-content-around">
      <EmptyCart />
    </div>

    <div v-else-if="carts" v-for="itr in len" :key="itr" class="row mt-1  pt-3 justify-content-around">
      <div class="col-2"></div>
      <div class="col-md-3 embed-responsive embed-responsive-16by9">
        <img v-bind:src="cartItem[itr-1].imgUrl" class="w-100 card-img-center embed-responsive-item">
      </div>
      <div class="col-md-5">
        <div class="card-block px-3">
          <h5 class="card-title" @click="showDetails(itr-1)">{{cartItem[itr-1].pName}}</h5>
          <!--          <p id="item-description" class="card-text font-italic mb-0">{{cartItem[itr-1].pDescription.substring(0,90)}}...</p>-->
          <!-- <p id="item-price" class="mb-0 font-weight-bold">R$ {{cartItem[itr-1].pPrice}} / unidade</p> -->
          <p class="mb-0 quantity">
            Quantidade:
            <input size="1" class="p-0 h-25 border-bottom border-top-0 border-left-0 border-right-0"
              v-model="cartItem[itr-1].pQuantity" @change="updateItem(cartItem[itr-1].id,cartItem[itr-1].pQuantity)" />
          </p>
          <p id="item-total-price" class="mb-2 mt-1">Preço total: R$ <span
              class="font-weight-bold">{{cartItem[itr-1].pPrice*cartItem[itr-1].pQuantity}}</span></p>
          <a href="#" class="text-right" style="color: red;" @click="deleteItem(cartItem[itr-1].id)"><i
              class="bi bi-x-circle" style="vertical-align: baseline"></i> Remover</a>

        </div>
        <div class="col-3"></div>
      </div>
      <div class="col-2"></div>
      <div class="col-12"></div>
      <div class="linha col"></div>
    </div>

    <div v-if="len != 0" class="row mt-1  pt-3 justify-content-around">
      <CalculaFrete @clickedFrete="passaValor($event)" />

      <br>
      <div class="total-cost pt-4 text-right">
        <h6>Frete: R$ {{ frete.valor }} </h6>
        <h4>Total: R$ {{ totalcost + parseInt(frete.valor) }}</h4>
        <button :disabled="isDisabled()" class="btn btn-primary confirm" @click="checkout()">Confirmar pedido</button>
      </div>
    </div>

  </div>
</template>

<script>
  import CalculaFrete from "../Frete/CalculaFrete.vue";
  import EmptyCart from './EmptyCart.vue';

  export default {
    name: 'Cart',
    components: {
      CalculaFrete,
      EmptyCart
    },
    props: ["baseURL"],
    data() {
      return {
        carts: null,
        token: null,
        len: 0,
        totalcost: 0,
        cartItem: [],
        Id: -1,
        frete: {},
      }
    },
    components: {
      CalculaFrete,
      EmptyCart
    },
    methods: {
      isDisabled() {
        if (this.len === 0) {
          return true;
        }
        return false;
      },

      showDetails(itr) {
        this.$router.push({
          name: 'ShowDetails',
          params: {
            id: this.cartItem[itr].pId
          }
        })
      },

      passaValor(frete) {
        this.frete = frete;
      },

      checkout() {
        this.$router.push({
          name: 'Checkout',
          params: {
            id: this.len
          }
        })
      },

      listCartItems() {
        axios.get(`${this.baseURL}cart/?token=${this.token}`).then((response) => {
            if (response.status == 200) {
              this.carts = response.data;
              this.len = Object.keys(this.carts.cartItems).length
              this.totalcost = this.carts.totalCost
              let i;
              for (i = 0; i < this.len; i++) {
                this.cartItem.push({
                  imgUrl: this.carts.cartItems[i].product.imageURL,
                  pName: this.carts.cartItems[i].product.name,
                  pDescription: this.carts.cartItems[i].product.description,
                  pPrice: this.carts.cartItems[i].product.price,
                  pQuantity: this.carts.cartItems[i].quantity,
                  id: this.carts.cartItems[i].id,
                  pId: this.carts.cartItems[i].product.id,
                  userId: this.carts.cartItems[i].userId
                })
              }
            }
          },
          (error) => {
            console.log(error)
          });

      },

      deleteItem(itemId) {
        axios.delete(`${this.baseURL}cart/delete/${itemId}/?token=${this.token} `)
          .then((response) => {
            if (response.status == 200) {
              this.$router.go(0);
            }
            this.$emit("fetchData");
          }, (error) => {
            console.log(error)
          })
      },

      updateItem(itemId, quantity) {
        let i
        for (i = 0; i < this.len; i++) {
          if (this.cartItem[i].id === itemId) {
            break
          }
        }
        this.cartItem[i].pQuantity = quantity
        let userId = this.cartItem[i].userId
        let productId = this.cartItem[i].pId
        axios.put(`${this.baseURL}cart/update/${itemId}/?token=${this.token}`, {
          id: itemId,
          userId,
          productId,
          quantity
        }).then(() => {
          this.listCartItems()
          this.$emit("fetchData");
        })

      }
    },

    mounted() {
      this.token = localStorage.getItem("token");
      this.listCartItems();

    },
  };
</script>

<style scoped>
  h4,
  h5 {
    font-family: 'Roboto', sans-serif;
    color: #484848;
    font-weight: 700;
  }

  .embed-responsive .card-img-top {
    object-fit: cover;
  }

  .embed-responsive {
    height: 200px;
  }

  .col-md-5 {
    align-self: center;
  }

  .linha {
    border-bottom: solid darkgrey;
    padding-bottom: 20px;
    border-width: 1px;
    margin-left: 10%;
    margin-right: 10%;
  }

  @media (max-width: 576px) {
    .card-img-center {
      object-fit: contain;
    }

    .card-title {
      font-size: 16px;
      margin-top: 10px;
      margin-bottom: 10px !important;
    }

    .card-block {
      text-align: center;
    }

    .quantity {
      font-size: 14px;
    }

    #item-total-price {
      font-weight: bold;
    }
  }
</style>