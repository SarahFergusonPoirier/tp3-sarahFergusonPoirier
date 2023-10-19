<template>
  <div class="container">
    <img :src="require(`@/assets/img/${product.photo}`)" alt="product.name">
    <h3>{{ product.name }}</h3>
    <p><span>Description: </span>{{ product.description }}</p>
    <p><span>Prix: </span>{{ product.price.toFixed(2) }}</p>
    <p><span>Category: </span>{{ product.category }}</p>
    <router-link class="btn btn-block" :to="'/product-edit/'+product.id">Éditer le produit</router-link>
  </div>
</template>

<script>
    export default {
        props: ['inventory'],
        computed: {
            product () {
                const product = this.inventory.find((p) => {
                    return p.name === this.$route.params.id
                })
                return product
            }, 
            index () {
                const index = this.inventory.findIndex((p) => {
                    return p.name === this.$route.params.id
                })
                return index
            }
        }
    }
</script>