<template>
  <div class="container">
    <div v-for="(product, i) in inventory" :key="product.id" class="produit">
      <img :src="require(`@/assets/img/${product.photo}`)" alt="product.name">
      <h3><router-link :to="{name: 'product', params: {id:product.name}}">{{ product.name }}</router-link></h3>
      <p><span>Description: </span>{{ product.description }}</p>
      <p><span>Prix: </span>{{ product.price.toFixed(2) }}</p>
      <p><span>Category: </span>{{ product.category }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ['inventory']
}
</script>
