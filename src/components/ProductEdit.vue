<template>
  <section>
    <div class="modal-body">
      <h2 class="heading">Edycja produktu: {{ productToUpdate.name }}</h2>
      <p>Nazwa produktu</p>
      <input type="text" v-model="nameInput" />
      <p>Cena</p>
      <input type="number" v-model="priceInput" />
      <p>Promocyjna cena</p>
      <input type="number" v-model="priceSaleInput" />
      <select v-model="currencyInput">
        <option v-for="currency in currencies" :key="currency.id" :value="currency.id">{{ showCurrency(currency.id) }}
        </option>
      </select>
      <button @click="handleUpdateButton">zapisz</button>
      <button @click="closeModal()">zamknij</button>
    </div>
    <div class="modal-backdrop" @click="closeModal()"></div>
  </section>
</template>

<script>
export default {
  props: {
    productToUpdate: {
      type: Object,
      required: true,
    }
  },
  inject: ['currencies', 'showCurrency', 'closeModal', 'updateProduct'],
  data() {
    return {
      nameInput: this.productToUpdate.name,
      priceInput: this.productToUpdate.price,
      priceSaleInput: this.productToUpdate.priceSale,
      currencyInput: this.productToUpdate.currencyId,
    }
  },
  methods: {
    handleUpdateButton() {
      console.log('no robie')
      this.updateProduct(this.productToUpdate.id, {
        name: this.nameInput,
        price: this.priceInput,
        priceSale: this.priceSaleInput,
        currencyId: this.currencyInput,
      })
    }
  },
}
</script>

<style scoped>
.modal-body {
  position: fixed;
  right: 0;
  top: 0;
  bottom: 0;
  width: 600px;
  padding: 1em;
  background: var(--color-background-container);
  box-shadow: 0 0 10px var(--color-background-backdrop);
  z-index: 2;
}

.modal-backdrop {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background: var(--color-background-backdrop);
  opacity: 0.5;
  z-index: 1;
}

.heading {
  margin-bottom: 15px;
  font-size: 14px;
}
</style>

