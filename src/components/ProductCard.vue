<template>
  <article class="container product-card">
    <h2 class="heading">{{ product.name }}</h2>
    <img :src="product.img" class="product-image" alt="product.name" />
    <div class="price-main">{{ productPrice }} {{ showCurrency(product.currencyId) }}</div>
    <div v-if="productPriceBefore" class="price-secondary">{{ productPriceBefore }} {{ showCurrency(product.currencyId) }}
    </div>
    <div v-if="product.priceSale" class="discount-bar">{{ productDiscount }}%</div>
  </article>
</template>

<script>
export default {
  props: {
    product: {
      type: Object,
      required: true,

    }
  },
  computed: {
    productPrice() {
      return this.product.priceSale ? this.product.priceSale : this.product.price;
    },
    productPriceBefore() {
      return this.product.priceSale ? this.product.price : null;
    },
    productDiscount() {
      return 100 - Math.ceil((this.product.priceSale / this.product.price * 100));
    }
  },
  inject: ['showCurrency']
}
</script>

<style scoped>
.product-card {
  cursor: pointer;
}

.heading {
  margin-bottom: 15px;
  font-weight: 600;
  font-size: 1rem;
  color: var(--color-heading)
}

.product-image {
  display: block;
  height: 200px;
  max-width: 90%;
  margin: 0 auto;
}

.price-main {
  margin: 10px auto;
  text-align: center;
  font-weight: 600;
  font-size: 1.2em;
  color: var(--color-active);
}

.price-secondary {
  margin-bottom: 10px;
  text-align: center;
  text-decoration: line-through;
}

.discount-bar {
  position: absolute;
  top: 8%;
  right: -20%;
  padding: 2px 100px;
  text-align: center;
  font-weight: 600;
  font-size: 0.9em;
  color: var(--color-text-discount);
  background-color: var(--color-background-discount-bar);
  transform: rotate(45deg);
}

@media (max-width: 1200px) {
  .product-image {
    max-height: 80%;
    width: auto;
  }

  .discount-bar {
    top: 15%;
    right: -8%;
  }
}

@media (max-width: 594px) {
  .discount-bar {
    top: 15%;
    right: -15%;
  }
}

@media (max-width: 380px) {
  .discount-bar {
    top: 10%;
    right: -24%;
  }
}
</style>

