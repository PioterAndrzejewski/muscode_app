<template>
  <section>
    <div class="modal-body">
      <h2 class="heading">Edycja produktu: {{ productToUpdate.name }}</h2>
      <img class="product-image" :src="productToUpdate.img" :alt="productToUpdate.name">
      <div class="inputs-wrapper">
        <p class="product-label">Nazwa produktu</p>
        <input type="text" v-model="nameInput" class="product-input" />
        <p class="product-label">Cena</p>
        <input type="number" v-model="priceInput" class="product-input" />
        <p class="product-label">Promocyjna cena</p>
        <input type="number" v-model="priceSaleInput" class="product-input" />
        <p class="product-label">Waluta</p>
        <select v-model="currencyInput" class="product-input">
          <option v-for="currency in currencies" :key="currency.id" :value="currency.id">{{ showCurrency(currency.id) }}
          </option>
        </select>
      </div>
      <div class="spacer">
        <div class="button-container">
          <button @click="handleUpdateButton" class="button">zapisz</button>
          <button @click="closeModal()" class="button">zamknij</button>
        </div>
      </div>
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
  display: flex;
  flex-direction: column;
  width: 600px;
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
  color: var(--color-heading);
  padding: 25px 12px;
  font-size: 1.4em;
  font-weight: 600;
  border-bottom: 4px solid var(--color-border-modal);
}

.product-image {
  display: block;
  margin: 45px auto 22px auto;
  object-fit: contain;
  width: 200px;
  height: 200px;
  border-radius: 50%;
  box-shadow: 0 0 4px var(--color-border)
}

.inputs-wrapper {
  padding-right: 16px;
}

.product-input {
  margin: 4px 6px 10px 6px;
  padding: 4px 6px;
  width: 100%;
  font-size: 0.9em;
  border: none;
  border-bottom: 1px solid var(--color-border);
}

.product-input:focus,
.product-input:hover {
  outline: none;
  border-bottom: 1px solid var(--color-active);
}

.product-label {
  margin: 0 10px;
  font-size: 0.85em;
}

.spacer {
  flex-grow: 1;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
}

.button-container {
  padding: 10px;
  border-top: 1px solid var(--color-border);
}

.button {
  padding: 10px 14px;
  color: var(--color-text);
  border: 1px solid var(--color-border-button);
  background: none;
  cursor: pointer;
}

.button:hover {
  color: var(--color-button-white);
  border: 1px solid var(--color-active);
  background-color: var(--color-active);
}

.button:nth-child(2) {
  margin-left: 6px;
}

@media (max-width: 1200px) {
  .modal-body {
    width: 100%;
    padding: 5%;
  }
}
</style>

