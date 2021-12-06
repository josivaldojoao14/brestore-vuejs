<template>
  <div class="adminPanel container">
      <router-link :to="{name : 'AdminProduct'}">
        <button type="button" class="btn btn-primary btn-lg">Adicione um produto</button>
      </router-link>
      <router-link :to="{name : 'AdminCategory'}">
        <button type="button" class="btn btn-primary btn-lg">Adicione categorias</button>
      </router-link> 
      <!--
      <router-link :to="{name : 'Gallery'}">
        <button type="button" class="btn btn-primary btn-lg">Galeria do ADM</button>
      </router-link> -->
  </div>
</template>

<script>
export default {
  mounted() {
    if (!localStorage.getItem('token')) {
      this.$router.push({name : 'Signin'});
    }
  }
}
</script>

<style>
.adminPanel{
  display : flex;
  flex-direction: column;
  align-items: center;
}
.adminPanel button{
  font-size: 22px;
  width: fit-content;
  margin: 25px;
}
</style>