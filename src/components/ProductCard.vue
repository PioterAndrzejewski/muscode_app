<template>
  <article class="container">
    <h2 class="heading">{{ product.name }}</h2>
    <img :src="product.img" class="product-image" />
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
.heading {
  margin-bottom: 15px;
  font-weight: 600;
  font-size: 1rem;
}

.product-image {
  display: block;
  height: 200px;
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
</style>

