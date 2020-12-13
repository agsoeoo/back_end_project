<template>




<div class="row justify-content-center"><div class="col-lg-10"><div class="card"><div class="card-body"><h4>Create an Order</h4> 
<form id="review-form" @submit.prevent="submitOrder">
    <div class="form-group"> <label for="ratinginput">Payment</label> 
   
    <select name="payment" id="paymentinput" required="required" class="form-control" v-model="payment">
        <option value="credit">Credit</option>
        <option value="debit">Debit</option>
    </select>
    </div> 
 
    <button type="submit" class="btn btn-primary">Submit Order</button>
    
    
     <button v-on:click="cancelOrder" type="clear" class="btn btn-outline-danger"> Cancel </button>

          <p v-if="errorMessage" class="form-text text-danger">{{errorMessage}}</p>
          
          </form></div></div></div></div>

</template>


<script>
import axios from 'axios';
export default {
    data(){
        return{
            payment:null,
            errorMessage:null,
        }
    },
  methods: {
    submitOrder(){
        const myOrder={
           payment: this.payment,
           productID: this.$route.params.pk
        };
        // console.log("Here is the order", myOrder)
        const token = this.$store.state.token;

        axios.post("/orders",myOrder,{
            headers:{
                Authorization: `Bearer ${token}`
            }
        })
        .then(()=>{this.$router.replace('/account')})
        .catch(()=>{this.errorMessage = "Unable to create an order, please try again later"})
    },
    cancelOrder(){
        this.$router.go(-1)
    }
  }
}
</script>

<style scoped>

</style>