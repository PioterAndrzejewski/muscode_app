<template>
  <header>
    <MainHeader msg="Muscode App" />
  </header>

  <main>
    <div class="wrapper">
      <TodoList class="height container" />
      <ProductsTable :products="products" />
      <ProductCard v-for="product in products" :key="product.id" class="height container" :product="product"
        @click="openModal(product.id)" />
    </div>
  </main>

  <aside>
    <ProductEdit v-if="modalOpened" :productToUpdate="productToUpdate" />
  </aside>
</template>

<script>
const currencies = [{
  id: 0,
  name: "$",
},
{
  id: 1,
  name: "PLN",
},
{
  id: 2,
  name: "EUR",
},
]
const productsInit = [
  {
    id: 0,
    name: "iPhone 6s Plus 16GB",
    price: 1000,
    priceSale: 649,
    currencyId: 0,
    img: '/img/img1.png'
  },
  {
    id: 1,
    name: "iPad Pro 32GB",
    price: 800,
    priceSale: 600,
    currencyId: 0,
    img: '/img/img2.png'
  },
  {
    id: 2,
    name: "MacBook Pro",
    price: 8000,
    priceSale: null,
    currencyId: 1,
    img: '/img/img3.png'
  },
];
import MainHeader from './components/MainHeader.vue';
import TodoList from './components/TodoList.vue';
import ProductsTable from './components/ProductsTable.vue';
import ProductCard from "./components/ProductCard.vue";
import ProductEdit from "./components/ProductEdit.vue";

export default {
  components: {
    MainHeader,
    TodoList,
    ProductsTable,
    ProductCard,
    ProductEdit,
  },
  data() {
    this.products = productsInit;
    return {
      modalOpened: false,
      productToUpdate: null,
    }
  },
  provide() {
    return {
      currencies,
      showCurrency: this.showCurrency,
      updateProduct: this.updateProduct,
      closeModal: this.closeModal,
      productToUpdate: this.productToUpdate,
    }
  },
  methods: {
    showCurrency(currencyId) {
      return currencies.find(el => el.id === currencyId).name;
    },
    updateProduct(productId, newProductData) {
      this.products = this.products.map(product => product.id === productId ? {
        ...product,
        ...newProductData,
      } : product)
      this.closeModal();
    },
    openModal(productId) {
      this.productToUpdate = this.products.find(product => product.id === productId);
      console.log(this.productToUpdate)
      this.modalOpened = true;
    },
    closeModal() {
      this.modalOpened = false;
    }
  }
}
</script>

<style>
/* variables */
:root {
  --color-background: #f5f8fa;
  --color-background-container: #fff;
  --color-background-discount-bar: #000;
  --color-background-backdrop: #000000d0;
  --color-border: #b2b2b2;
  --color-border-container: #b2b2b296;
  --color-border-hover: var(--vt-c-divider-light-1);

  --color-heading: #333;
  --color-text: #384a5c;
  --color-text-discount: #fff;
  --color-active: #862583;

  --font-family: Roboto, sans-serif;

  --width-container: 1180px;
}

*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
  font-weight: normal;
}

body {
  color: var(--color-text);
  background: var(--color-background);
  font-family: var(--font-family);
  font-size: 14px;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.container {
  position: relative;
  overflow: hidden;
  padding: 22px;
  background-color: var(--color-background-container);
  border-radius: 5px;
  box-shadow: 0 0 10px var(--color-border-container);
}

.wrapper {
  margin: 0 auto;
  max-width: 1180px;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 15px;
}

.second-element {
  grid-column-start: 2;
  grid-column-end: -1;
}

.height {
  min-height: 200px;
}
</style>
