<template>
  <section class="container second-element height container">
    <h2 class="heading">Lista produktów</h2>

    <table>
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
          <td>{{ product.price }}</td>
          <td>{{ product.priceSale }}</td>
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

<style scoped></style>