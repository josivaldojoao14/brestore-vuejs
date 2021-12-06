<template>
  <div class="row mt-5">
  <div class="col-2"></div>
    <form>
      <div class="form-group">
        <label>Insira seu CEP</label>
        <input type="text" class="form-control w-50" v-model="cepDestino" required>
      </div>
      <button type="button" class="btn btn-primary" @click="calcFrete" data-toggle="collapse"
        data-target="#collapseExample" aria-expanded="false" aria-controls="collapseExample">Calcular</button>
    </form>
    <div class="col collapse" id="collapseExample">
      <div class="card card-body" style="width: 100%;">
        <p><b>Tipo de entrega:</b> PAC</p>
        <p><b>Valor do frete:</b> R$ {{ frete.valor }}</p>
        <p><b>Prazo de entrega:</b> {{ frete.prazo }} úteis</p>
      </div>
    </div>
    <div class="col-2"></div>
  </div>
</template>


<script>
  export default {
    name: "CalculaFrete",
    data() {
      return {
        frete: []
      }
    },
    props: ["baseURL2"],
    methods: {
      async calcFrete() {
        const newFrete = {
          cepDestino: this.cepDestino,
          servico: "04510",
          cepOrigem: "50030220",
          formato: "1",
          comprimento: 20.0,
          altura: 5.0,
          largura: 20.0,
          diametro: 0.0,
          peso: 0.3
        }

        await axios({
            method: 'post',
            url: "https://gabrielidsm-fretecorreios.herokuapp.com/correios/frete",
            data: JSON.stringify(newFrete),
            headers: {
              'Content-Type': 'application/json'
            }
          })
          .then(res => {
            this.frete = res.data;
            this.$emit('clickedFrete', this.frete);
          })
          .catch(err => console.log(err));
      }
    }
  }
</script>

<style scoped>
  h4 {
    font-family: 'Roboto', sans-serif;
    color: #484848;
    font-weight: 700;
  }

  .card-body {
    -webkit-box-flex: 1;
    -ms-flex: 1 1 auto;
    flex: 1 1 auto;
    padding: 1.25rem;
    width: 60%;
    padding: 10px;
    text-align: center;
    margin: 0;
  }

  .card.card-body p {
    margin: 5px;
  }
</style>