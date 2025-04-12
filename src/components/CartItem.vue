<template>
  <div class="cart-item">
    <img :src="item.product.images[0].replace('300x200', '100x100')" alt="Product" />
    <div class="details">
      <h3>{{ item.product.name }}</h3>
      <p>{{ item.product.price }} ₽ x {{ item.quantity }} = {{ item.product.price * item.quantity }} ₽</p>
      <div class="quantity">
        <button @click="updateQuantity(-1)">-</button>
        <span>{{ item.quantity }}</span>
        <button @click="updateQuantity(1)">+</button>
      </div>
      <button class="btn btn-danger" @click="removeItem">Удалить</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    item: Object
  },
  methods: {
    updateQuantity(change) {
      const newQuantity = this.item.quantity + change;
      this.$store.commit('updateCartQuantity', { productId: this.item.product.id, quantity: newQuantity });
    },
    removeItem() {
      this.$store.commit('removeFromCart', this.item.product.id);
    }
  }
};
</script>

<style scoped>
.cart-item {
  display: flex;
  align-items: center;
  background: #F8F5F2;
  border-radius: 15px;
  padding: 20px;
  margin-bottom: 20px;
  box-shadow: 0 2px 6px rgba(47, 47, 47, 0.1);
  transition: all 0.3s ease;
}

.cart-item:hover {
  box-shadow: 0 6px 12px rgba(47, 47, 47, 0.15);
}

.cart-item img {
  width: 100px;
  height: 100px;
  object-fit: cover;
  border-radius: 8px;
}

.details {
  flex: 1;
  margin-left: 20px;
}

h3 {
  font-size: 18px;
  color: #2F2F2F;
  font-weight: 500;
}

p {
  font-size: 16px;
  color: #6D8299;
}

.quantity {
  display: flex;
  align-items: center;
  gap: 10px;
  margin: 10px 0;
}

.quantity button {
  background: #F4A7A9;
  color: #F8F5F2;
  border: none;
  padding: 5px 10px;
  border-radius: 5px;
  font-weight: 500;
  transition: all 0.3s ease;
}

.quantity button:hover {
  background: #E8C6B5;
}

.btn-danger {
  background: #F4A7A9;
  color: #F8F5F2;
  padding: 8px 16px;
  border: none;
  border-radius: 8px;
  font-weight: 500;
  transition: all 0.3s ease;
}

.btn-danger:hover {
  background: #E8C6B5;
}

@media (max-width: 768px) {
  .cart-item {
    flex-direction: column;
    text-align: center;
  }
  .details {
    margin-left: 0;
    margin-top: 10px;
  }
}
</style>