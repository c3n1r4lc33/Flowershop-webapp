<template>
    <div class="cart">
      <h2>Корзина</h2>
      <div v-if="cart.length">
        <cart-item v-for="item in cart" :key="item.product.id" :item="item" />
        <p class="total">Итого: {{ total }} ₽</p>
        <button class="btn btn-primary" @click="$router.push('/checkout')">Оформить заказ</button>
      </div>
      <p v-else>Корзина пуста</p>
    </div>
  </template>
  
  <script>
  import CartItem from '../components/CartItem.vue';
  
  export default {
    components: { CartItem },
    computed: {
      cart() {
        return this.$store.state.cart;
      },
      total() {
        return this.$store.getters.cartTotal;
      }
    }
  };
  </script>
  
  <style scoped>
  .cart {
    padding-bottom: 40px;
  }
  .cart-item {
    background: #E8D9CF;
    color: #6D8299;

  }
  h2 {
    text-align: center;
    margin-bottom: 30px;
    font-weight: 600;
  }
  
  .total {
    font-size: 20px;
    text-align: right;
    margin: 20px 0;
    color: #6D8299;
  }
  
  .btn-primary {
    display: block;
    width: 200px;
    margin: 0 auto;
    background: #F4A7A9;
    color: #F8F5F2;
    padding: 12px;
    border: none;
    border-radius: 10px;
    font-size: 16px;
    font-weight: 500;
    transition: all 0.3s ease;
  }
  
  .btn-primary:hover {
    background: #E8C6B5;
    box-shadow: 0 4px 8px rgba(47, 47, 47, 0.2);
  }
  
  p {
    text-align: center;
    font-size: 18px;
    color: #6D8299;
  }
  </style>