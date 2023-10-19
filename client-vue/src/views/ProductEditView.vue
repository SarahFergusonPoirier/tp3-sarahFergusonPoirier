<template>
    <div class="container">
        <div novalidate v-if="!submitted">
            <div class="form-control">
                <label>Nom du produit</label>
                <input type="text" placeholder="Ajouter un produit" id="name" v-model="product.name" required />
            </div>
            <div class="form-control">
                <label>Description</label>
                <textarea id="productDescription" v-model="product.description" placeholder=""></textarea>
            </div>
            <div class="form-control">
                <label>Prix</label>
                <input type="text" placeholder="Ajouter un prix" id="productPrice" v-model.number="product.price" required/>
            </div>
            <div class="form-control">
                <label>Chemin vers la photo</label>
                <input type="text" placeholder="Ajouter un chemin vers la photo" id="photo" v-model="product.photo" required />
            </div>
            <div class="form-control">
                <label>Catégorie</label>
                <select id="productCategory" v-model="product.category" placeholder="Ajouter une catégorie" required>
                    <option value="">Select</option>
                    <option value="electroniques">Électroniques</option>
                    <option value="meubles">Meubles</option>
                    <option value="vetements">Vêtements</option>
                </select>
            </div>
            <button class="btn btn-block" type="button" @click="updateProduct">Éditer le produit</button>
        </div>
        <div v-if="submitted">
            <p>Produit modifié!</p>
            <button class="btn btn-block" type="button" @click="editProduct">Éditer le produit</button>
            <button class="btn btn-danger" type="button" @click="deleteProduct">Supprimer le produit</button>
        </div>
    </div>
</template>

<script>
    import ProductDataService from '@/services/ProductDataService'
    export default {
        props: ['removeInventory', 'inventory', 'remove', 'updateInventory'],
        data () {
            return {
                message: null, 
                submitted: false, 
                product: {},
                id: parseInt(this.$route.params.id)
            }
        },
        methods: {
            updateProduct () {
                ProductDataService.update(this.id, this.product)
                .then(response => {
                    this.updateInventory(this.productIndex, this.product)
                    this.submitted = true
                    this.message = response.data.message
                })
            },
            deleteProduct () {
                ProductDataService.delete(this.id)
                    .then(response => {
                        this.removeInventory(this.productIndex)
                        this.$router.push({ name: 'home' })
                    })
            },
            editProduct () {
                this.submitted = false
            }
        },
        computed: {
            productIndex () {
                const index = this.inventory.findIndex((p) => {
                    return p.id === this.id
                })
                return index 
            }
        },
        mounted () {
            ProductDataService.get(this.id)
                .then(response => {
                    this.product = response.data
                })
        }
    }
</script>