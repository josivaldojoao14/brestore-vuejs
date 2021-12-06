<template>
  <div class="geral mt-5">
    <h3 class="title">Confirme a compra clicando no botão</h3>
        <button class="btn-primary" @click="goToCheckout()">
            Confirmar a compra
        </button>
        <br>
        <br>
        <button class="btn-primary"><router-link class="text-light" :to="{name : 'Order'}">
            Ir para meu pedidos <i class="bi bi-arrow-right"></i>
        </router-link></button>
        
  </div>
</template>
<script>
export default {
    data(){
        return {
            stripeAPIToken: process.env.VUE_APP_STRIPETOKEN,
            stripe: '',
            token:null,
            sessionId:null,
            checkoutBodyArray:[]
            }
    },
    name:'Checkout',
    props:["baseURL"],
    methods: {
        
        getAllItems(){
            axios.get(`${this.baseURL}cart/?token=${this.token}`).then((response) => {
                if(response.status==200){
                    let products = response.data
                    let len=Object.keys(products.cartItems).length
                    for(let i=0;i<len;i++)
                        this.checkoutBodyArray.push({
                            imageUrl:products.cartItems[i].product.imageURL,
                            productName:products.cartItems[i].product.name,
                            quantity:products.cartItems[i].quantity,
                            price:products.cartItems[i].product.price,
                            productId:products.cartItems[i].product.id,
                            userId:products.cartItems[i].userId
                    })
                }
            },err=>{
                console.log(err)
            })
        },
        goToCheckout(){
            axios.post(`${this.baseURL}order/add/?token=${this.token}`)
            .then(response => {
                this.token = response.data
                swal({
                    text: "Pedido realizado com sucesso!",
                    icon: "success",
                    closeOnClickOutside: false,
                    });
            },
            (err)=>{
                console.log(err)
            })
        }
    },
    mounted(){
        // get the token
        this.token = localStorage.getItem("token");
        if(typeof( this.$route.params.id) === "undefined"){
            this.$router.push({name:'Home'})
        }
        
        this.getAllItems()
    },
}
</script>

 <style >
.geral{
    text-align: center;
}

.title{
margin-bottom: 20px;

}

</style>