<template>
<center>
<div class="card ">
  <img src="https://www.collinsdictionary.com/images/full/apple_158989157.jpg" alt="Avatar" style="width:30%; margin-top:5%;">
  <div class="container">
    <h4><b>Apple</b></h4> 
    <p>Good for health</p> 
    <stripe-checkout
      ref="checkoutRef"
      mode="payment"
      :pk="publishableKey"
      :line-items="lineItems"
      :success-url="successURL"
      :cancel-url="cancelURL"
      @loading="v => loading = v"
    />
    <button class="button button4"  @click="submit">Buy now</button>
  </div>
</div>
</center>
</template>
<script>
import { StripeCheckout } from '@vue-stripe/vue-stripe';

export default ({
  components: {
    StripeCheckout,
  },
  data() {
    return{
      publishableKey:'your_publishable_key',
      successURL:'http://localhost:8080/success',
      cancelURL:'http://localhost:8080/error',
      loading: false,
      lineItems: [
        {
          price: 'your_price_id',
          quantity: 1,
        },
      ],
    }
  },
  methods: {
    submit () {
      // You will be redirected to Stripe's secure checkout page
      this.$refs.checkoutRef.redirectToCheckout();
    },
  }
})
</script>

<style>
.card {
  margin-top: 13%;;
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  transition: 0.3s;
  width: 40%;
  background-color:rgb(242, 239, 239);
}

.card:hover {
  box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
}

.container {
  padding: 2px 16px;
}
.button {
  background-color: #04AA6D; /* Green */
  border: none;
  color: white;
  padding: 20px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
}
.button4 {border-radius: 12px;}
</style>