<template>
  <div class="header">
    <h1 class="green">{{ msg }}</h1>
  </div>
</template>

<script setup>
defineProps({
  msg: {
    type: String,
    required: true
  }
})
</script>

<style scoped>
.header h1 {
  margin: 46px 0;
  font-weight: 600;
  font-size: 2.2em;
  text-align: center;
}
</style>
