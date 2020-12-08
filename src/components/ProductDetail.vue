<template>
    <div>
            <div class="card">
                    <div class="card-body">
                        <h2 class="text-primary">{{product.productName}}</h2>
                        <br/>
                        <p>Price: <br/> <strong>{{formattedPrice}}</strong></p>
                        <p>Cateogory: <br/> <strong>{{product.CategoryName}}</strong></p>
                       
                    </div>
            </div>

            <br/>
            <router-link v-if="auth" :to="`/products/${this.$route.params.pk}/orders`">
                <button type="button" class="btn btn-success">Add to Cart</button>
            </router-link>
              <router-link v-else :to="`/signin`">
                <button type="button" class="btn btn-outline-success">Sign In to Add to Cart</button>
            </router-link>

    </div>
</template>


<script>
export default {
    computed:{
        product(){
            var products = this.$store.state.products;
            var thisProduct = products.find((aProduct)=> aProduct.ProductID == this.$route.params.pk)

            console.log("Here is the product y ou want", thisProduct);
            return thisProduct
        },
        formattedPrice(){
            return new Intl.NumberFormat("en-US",{
                style: 'currency',
                currency: 'USD'
            }).format(this.product.productPrice)
        },
        auth(){return this.$store.state.token}
    }
    
}
</script>

<style scoped>

</style>