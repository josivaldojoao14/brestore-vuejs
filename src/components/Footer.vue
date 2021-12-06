<template>
  <footer>
    <div class="container pt-5">
      <div class="row">
        <div class="col-md-3 col-4">
          <ul style="list-style-type: none">
            <li class="text-light font-weight-bold pb-2">Conheça a gente</li>
            <li><a class="footer-link font-weight-light" href="#">Sobre nós</a></li>
            <li><a class="footer-link font-weight-light" href="#">Android App</a><br></li>
            <li><a class="footer-link font-weight-light" href="#">iOS App</a><br></li>
          </ul>
        </div>

        <div class="col-md-3 col-4">
          <ul style="list-style-type: none">
            <li class="text-light font-weight-bold">Fique conectado com a gente</li>
            <li><a class="footer-link font-weight-light" href="#">Facebook</a></li>
            <li><a class="footer-link font-weight-light" href="#">Twitter</a><br></li>
            <li><a class="footer-link font-weight-light" href="#">Instagram</a><br></li>
          </ul>
        </div>

        <div class="col-md-3 col-4">
          <ul style="list-style-type: none">
            <li class="text-light font-weight-bold">Suporte</li>
            <li><a class="footer-link font-weight-light" href="#">Central de reembolsos</a></li>
            <li><a class="footer-link font-weight-light" href="#">Proteção de compra</a><br></li>
            <li><a class="footer-link font-weight-light" href="#">Ajuda</a><br></li>
          </ul>
        </div>
        <div class="col-md-3 col-5">
          <div class="row">
          <div class="col-12">
            <div class="text-center">
              <img id="logo" src="../assets/logoPink.png" />
            </div>
          </div>
        </div>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name : "Footer"
}
</script>

<style>
footer {
  margin-top : 100px;
  background-color:#00453d;
  font-size:16px;
}

li {
  padding-left: 0;
  padding-bottom: 10px;
}

a {
  text-decoration: none;
}

.footer-link {
  color: #DDD;
}

#logo {
  width: 150px;
}

footer {
  font-family: 'Roboto', sans-serif;
}


</style>
