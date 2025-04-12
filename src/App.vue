<template>
  <div class="app">
    <header class="header" :class="{ scrolled: isScrolled }">
      <div class="container">
        <router-link to="/" class="logo" @click="refreshPage">
          <img src="/images/logo.svg" alt="Логотип" />
        </router-link>
        <nav class="nav" :class="{ hidden: isScrolled }">
          <router-link to="/">Главная</router-link>
          <router-link to="/catalog">Каталог</router-link>
          <router-link to="/about">О нас</router-link>
          <router-link to="/contacts">Контакты</router-link>
          <router-link to="/gallery">Галерея</router-link>
          <div class="search-bar">
            <input
              v-model="searchQuery"
              @input="filterProducts"
              placeholder="Поиск..."
            />
            <svg
              class="search-icon"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
            >
              <circle cx="11" cy="11" r="8" />
              <line x1="21" y1="21" x2="16.65" y2="16.65" />
            </svg>
            <div class="suggestions" v-if="suggestions.length">
              <p
                v-for="suggestion in suggestions"
                :key="suggestion.id"
                @click="selectSuggestion(suggestion)"
              >
                {{ suggestion.name }}
              </p>
            </div>
          </div>
          <router-link to="/cart" class="cart-link">
            <svg
              class="cart-icon"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
            >
              <path d="M6 2L3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4z" />
              <path d="M3 6h18" />
              <path d="M16 10a4 4 0 0 1-8 0" />
            </svg>
            <span v-if="cartCount" class="cart-count">{{ cartCount }}</span>
          </router-link>
        </nav>
      </div>
    </header>
    <main class="main">
      <router-view />
    </main>
    <footer-vue />
  </div>
</template>

<script>
import FooterVue from "./components/Footer.vue";

export default {
  name: "App",
  components: { FooterVue },
  data() {
    return {
      searchQuery: "",
      suggestions: [],
      isScrolled: false,
    };
  },
  computed: {
    cartCount() {
      return this.$store.state.cart.length;
    },
  },
  mounted() {
    window.addEventListener("scroll", this.handleScroll);
  },
  beforeDestroy() {
    window.removeEventListener("scroll", this.handleScroll);
  },
  methods: {
    handleScroll() {
      if (window.scrollY > 50) {
        this.isScrolled = true;
      } else if (window.scrollY < 25) {
        this.isScrolled = false;
      } // Скрываем нав после 50px скролла
    },
    filterProducts() {
      if (this.searchQuery) {
        this.suggestions = this.$store.state.products.filter((p) =>
          p.name.toLowerCase().includes(this.searchQuery.toLowerCase())
        );
      } else {
        this.suggestions = [];
      }
    },
    selectSuggestion(product) {
      this.$router.push(`/product/${product.id}`);
      this.searchQuery = "";
      this.suggestions = [];
    },
    refreshPage(event) {
      event.preventDefault();
      if (this.$route.path === "/") {
        window.scrollTo({ top: 0, behavior: "smooth" });
        window.location.reload();
      } else {
        this.$router.push("/").then(() => {
          window.scrollTo({ top: 0, behavior: "smooth" });
        });
      }
    },
  },
};
</script>

<style>
/* Глобальные стили без scoped */
body {
  margin: 0;
  padding: 0;
}

.app {
  background-color: #e8d9cf;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  font-family: "Open Sans", sans-serif;
  color: #2a2a2a;
}

h1,
h2,
h3 {
  font-family: "Playfair Display", serif;
  color: #2a2a2a;
}

p {
  font-family: "Open Sans", sans-serif;
  color: #5a7a6f;
}

button {
  font-family: "Open Sans", sans-serif;
  background: #f28c8c;
  color: #e8d9cf;
  padding: 10px;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  font-weight: 600;
  transition: all 0.3s ease;
}

button:hover {
  background: #e8b5a4;
}
</style>

<style scoped>
/* Стили только для хедера */
.header {
  background: #e8d9cf;
  padding: 20px 0;
  box-shadow: 0 2px 8px rgba(42, 42, 42, 0.1);
  position: sticky;
  top: 0;
  z-index: 10;
  transition: padding 0.3s ease;
}

.header.scrolled {
  padding: 10px 0; /* Уменьшаем padding при скролле */
}

.container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

.logo {
  position: relative;
  z-index: 11; /* Логотип всегда сверху */
}

.logo img {
  width: 150px;
  height: 50px;
  object-fit: contain;
  transition: transform 0.3s ease;
}

.logo:hover img {
  transform: scale(1.05); /* Легкое увеличение при наведении */
}

.nav {
  display: flex;
  align-items: center;
  transition: opacity 0.3s ease, transform 0.3s ease;
}

.nav.hidden {
  opacity: 0;
  transform: translateY(-100%); /* Уходит вверх при скролле */
  pointer-events: none; /* Отключаем взаимодействие */
}

.nav a {
  margin-left: 40px;
  color: #5a7a6f;
  text-decoration: none;
  font-size: 16px;
  font-weight: 500;
  transition: color 0.3s ease;
}

.nav a:hover {
  color: #f28c8c;
}

.search-bar {
  position: relative;
  margin-left: 40px;
}

.search-bar input {
  padding: 10px 40px 10px 15px;
  border: 2px solid #f28c8c;
  border-radius: 20px;
  font-size: 14px;
  background: #e8d9cf;
  color: #5a7a6f;
  width: 200px;
  transition: width 0.3s ease;
}

.search-bar input:focus {
  border-color: #e8b5a4;
  outline: none;
  box-shadow: 0 0 8px rgba(232, 181, 164, 0.2);
}

.search-icon {
  position: absolute;
  right: 10px;
  top: 50%;
  transform: translateY(-50%);
  width: 20px;
  height: 20px;
  color: #5a7a6f;
}

.suggestions {
  position: absolute;
  top: 100%;
  left: 0;
  background: #e8d9cf;
  border: 1px solid #f28c8c;
  border-radius: 10px;
  width: 100%;
  max-height: 200px;
  overflow-y: auto;
  box-shadow: 0 4px 8px rgba(42, 42, 42, 0.1);
  z-index: 20;
}

.suggestions p {
  padding: 8px;
  cursor: pointer;
  color: #5a7a6f;
  transition: background 0.3s ease;
}

.suggestions p:hover {
  background: #f28c8c;
  color: #e8d9cf;
}

.cart-link {
  display: flex;
  align-items: center;
  margin-left: 40px;
  position: relative;
}

.cart-icon {
  width: 26px;
  height: 26px;
  color: #5a7a6f;
  transition: color 0.3s ease;
}

.cart-link:hover .cart-icon {
  color: #f28c8c;
}

.cart-count {
  position: absolute;
  top: -10px;
  right: -10px;
  background: #f28c8c;
  color: #e8d9cf;
  font-size: 12px;
  padding: 2px 6px;
  border-radius: 50%;
}

.main {
  flex: 1;
  padding: 40px 0;
}

@media (max-width: 768px) {
  .container {
    flex-direction: column;
    text-align: center;
  }
  .nav {
    margin-top: 20px;
    flex-wrap: wrap;
    justify-content: center;
  }
  .nav a,
  .search-bar,
  .cart-link {
    margin: 10px 20px;
  }
  .search-bar input {
    width: 100%;
    max-width: 300px;
  }
}
</style>
