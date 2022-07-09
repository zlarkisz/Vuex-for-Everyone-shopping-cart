<template>
  <div>
    <h1>Shopping Cart</h1>

    <ul>
      <li v-for="product in products" :key="product.id">
        {{ product.title }} - {{ $filters.currency(product.price) }} - {{ product.quantity }}
      </li>
    </ul>

    <p>{{ $filters.currency(total) }}</p>

    <button @click="checkout">Checkout</button>

    <p v-if="checkoutStatus" >{{ checkoutStatus }}</p>
  </div>
</template>

<script>
  import { mapState, mapGetters, mapActions } from 'vuex'

  export default {
    name: 'ShoppingCart',

    computed: {
      ...mapGetters('cart', {
        products: 'cartProducts',
        total: 'cartTotal'
      }),

      ...mapState('cart', {
        checkoutStatus: state => state.checkoutStatus
      })
    },

    methods: {
      ...mapActions('cart', [ 'checkout'])
    },
  }
</script>

<style lang="scss" scoped>

</style>