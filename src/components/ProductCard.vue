<template>
  <div class="product-card" @click="$router.push(`/product/${product.id}`)">
    <div class="image-wrapper">
      <img
        :src="product.images[0]"
        alt="Product"
        class="default-image"
        loading="lazy"
      />
      <img
        :src="product.images[1]"
        alt="Product"
        class="hover-image"
        loading="lazy"
      />
    </div>
    <div class="content-wrapper">
      <h3>{{ product.name }}</h3>
      <p>{{ product.price }} ₽</p>
      <button class="btn" @click.stop="addToCart">В корзину</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    product: Object
  },
  methods: {
    addToCart() {
      this.$store.commit('addToCart', { product: this.product, quantity: 1 });
    }
  }
};
</script>

<style scoped>
.product-card {
  background: #E8D9CF; /* Светлый фон карточки */
  border-radius: 15px;
  box-shadow: 0 4px 8px rgba(42, 42, 42, 0.1);
  overflow: hidden;
  transition: all 0.3s ease;
  position: relative;
  width: 100%;
  height: 350px; /* Фиксированная высота карточки */
  cursor: pointer;
}

.product-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 16px rgba(42, 42, 42, 0.15);
}

.image-wrapper {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 200px; /* Начальная высота изображения */
  overflow: hidden;
  transition: height 0.4s ease;
}

.product-card:hover .image-wrapper {
  height: 100%; /* Изображение растёт при наведении */
}

.image-wrapper img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  position: absolute;
  top: 0;
  left: 0;
  transition: opacity 0.4s ease, transform 0.4s ease;
}

.default-image {
  opacity: 1;
  transform: scale(1);
}

.hover-image {
  opacity: 0;
  transform: scale(1.1);
}

.product-card:hover .default-image {
  opacity: 0;
  transform: scale(1.1);
}

.product-card:hover .hover-image {
  opacity: 1;
  transform: scale(1);
}

.content-wrapper {
  position: absolute;
  bottom: 0;
  width: 100%;
  padding: 15px; /* Простой padding, кнопка на месте */
  background: #E8D9CF; /* Защита от просвечивания изображения */
  transition: opacity 0.4s ease;
}

.product-card:hover .content-wrapper {
  opacity: 0; /* Текст и кнопка исчезают */
}

h3 {
  font-family: 'Helvetica', sans-serif;
  font-size: 18px;
  color: #2A2A2A; /* Тёмный текст */
  font-weight: 500;
  margin-bottom: 5px;
}

p {
  font-family: 'Helvetica', sans-serif;
  font-size: 16px;
  color: #5A7A6F;
  margin-bottom: 10px;
}

.btn {
  display: block;
  width: 80%;
  margin: 0 auto;
  background: #F28C8C; /* Цвет кнопки */
  color: #E8D9CF;
  padding: 10px;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  font-weight: 500;
  transition: all 0.3s ease;
}

.btn:hover {
  background: #E8B5A4;
  transform: scale(1.05);
}

@media (max-width: 768px) {
  .product-card {
    height: 300px;
  }
  .image-wrapper {
    height: 150px;
  }
}
</style>