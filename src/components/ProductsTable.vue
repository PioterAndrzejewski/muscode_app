<template>
  <section class="container table-wrapper">
    <h2 class="heading">Lista produktów</h2>

    <table class="products-table">
      <thead>
        <tr>
          <th>#</th>
          <th>NAZWA</th>
          <th>PROMOCYJNA CENA</th>
          <th>CENA</th>
          <th>WALUTA</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="product in products" :key="product.id">
          <td>{{ product.id }}</td>
          <td>{{ product.name }}</td>
          <td>{{ product.priceSale }}</td>
          <td>{{ product.price }}</td>
          <td>{{ showCurrency(product.currencyId) }}</td>
        </tr>
      </tbody>
    </table>
  </section>
</template>

<script>
export default {
  props: {
    products: {
      type: Object,
      required: true,
    }
  },
  inject: ['showCurrency'],
}
</script>

<style scoped>
.table-wrapper {
  grid-column: 2 / -1;
}

.heading {
  font-size: 1.2em;
  font-weight: 600;
  margin-bottom: 26px;
  color: var(--color-heading);
}


.products-table {
  width: 100%;
  border-collapse: collapse;
}

.products-table tr {
  padding: 10px;
  border-bottom: 1px solid var(--color-border);
}

.products-table tr:hover {
  background-color: var(--color-background)
}

.products-table th {
  padding: 7px 0 10px 12px;
  text-align: left;
  font-size: 0.8em;
}

.products-table td {
  padding: 7px 0 10px 12px;
  font-size: 0.9em;
}


@media (max-width: 1200px) {
  .table-wrapper {
    grid-column: 1 / -1;
  }
}
</style>