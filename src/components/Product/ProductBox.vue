<template>

  <div class="card h-100 w-100">
    <router-link :to="{ name: 'ShowDetails', params: { id: product.id } }">
    <div class="embed-responsive embed-responsive-16by9">
      <img
        class="card-img-top embed-responsive-item"
        :src="product.imageURL"
        alt="Product Image"
      />
    </div>
    </router-link >
    <div class="card-body text-center p-2">
      <router-link :to="{ name: 'ShowDetails', params: { id: product.id } }">
        <h5 class="card-title">{{ product.name }}</h5>
      </router-link >

      <p class="card-text p-1 m-0 text-center preco">R$ {{ product.price }}</p>
      <router-link
        id="edit-product"
        :to="{ name: 'EditProduct', params: { id: product.id } }"
        v-show="$route.name == 'AdminProduct'"
      >
        Editar
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProductBox",
  props: ["product"],
  methods: {
    showDetails() {
      this.$router.push({
        name: "ShowDetails",
        params: { id: this.product.id },
      });
    },
  },
};
</script>


<style scoped>
a {
  text-decoration: none;
}

.embed-responsive{
  height: 260px;
}

.card-title {
  color: #484848;
  font-size: 1.1rem;
  font-weight: 400;
}

.card-title:hover {
  font-weight: bold;
}

.card-text {
  font-size: 0.9rem;
}

#edit-product {
  float: right;
}

.preco {
  color: black;
  font-size: 20px;
}

@media (max-width: 576px){

.embed-responsive{
height: 150px;
}

.card-img-top{
height: 100%;
}

.card-title{
  font-size: 15px;
}

.preco{
  font-size: 18px;
}

}

</style>
