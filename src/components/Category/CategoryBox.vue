<template>
  <div class="card h-100 w-100">
    <router-link :to="{ name: 'ListProducts', params: { id: category.id } }">
        <div class="embed-responsive embed-responsive-16by9">
          <img
            class="card-img-top embed-responsive-item"
            :src="category.imageUrl"
            alt="Category Image"
          />
        </div>  
    </router-link>

    <div class="card-body text-center p-1">
      <router-link :to="{ name: 'ListProducts', params: { id: category.id } }">
      <h5 class="card-title text">{{ category.categoryName }}</h5>
      </router-link>
    
      <router-link
        id="edit-category"
        :to="{ name: 'EditCategory', params: { id: category.id } }"
        v-show="$route.name == 'AdminCategory'"
      >
        Editar
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "CategoryBox",
  props: ["category"],
  methods: {
    listProducts() {
      this.$router.push({
        name: "ListProducts",
        params: { id: this.category.id },
      });
    },
  },
};
</script>

<style scoped>
.embed-responsive .card-img-top {
  object-fit: cover;
}

a {
  text-decoration: none;
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

#edit-category {
  float: right;
}


@media (max-width: 576px){

.card-title{
  font-size: 15px;
  margin-bottom: 0 !important;
}

}
</style>
