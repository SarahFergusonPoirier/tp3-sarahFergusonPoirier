<template>
    <nav>
        <router-link aria-current="page" to="/">Articles</router-link>
        <router-link to="/about">À propos</router-link>
        <router-link to="/product-add">Ajouter un produit</router-link>
    </nav>
    <header>

    </header>
    <router-view
    :inventory = "inventory"
    :addInventory = "addInventory"
    :removeInventory = "removeInventory"
    :updateInventory = "updateInventory"
    />
</template>

<script>
import ProductDataService from '@/services/ProductDataService'
export default {
  data () {
    return {
      inventory: []
    }
  },
  methods: {
    addInventory (data) {
      this.inventory.push(data)
    }, 
    removeInventory (index) {
      this.inventory.splice(index, 1)
    },
    updateInventory (index,data) {
      this.inventory[index].name = data.name
      this.inventory[index].description = data.description
      this.inventory[index].price = data.price 
      this.inventory[index].photo = data.photo
      this.inventory[index].category = data.category
    }
  },
  mounted () {
    ProductDataService.getAll()
      .then(response => {
        this.inventory = response.data
      })
  }
}
</script>