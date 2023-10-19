<template>
    <div class="container">
        <div v-if="!submitted">
            <div v-show="message">{{message}}</div>
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
            <button class="btn btn-block" type="button" @click="saveProduct">Ajouter le produit</button>
        </div>
        <div v-else>
            <p>Produit ajouté!</p>
            <button class="btn btn-block" type="button" @click="newProduct">Ajouter un nouveau produit</button>
        </div>
    </div>
</template>

<script>
    import ProductDataService from '@/services/ProductDataService'
    export default {
        props: ['addInventory'],
        data () {
            return {
                message: null, 
                submitted: false, 
                product: {
                    name: '',
                    description: '',
                    price: '',
                    photo: '',
                    category: '' 
                }
            }
        },
        methods: {
            saveProduct () {
                ProductDataService.create(this.product)
                .then(response => {
                    this.product.id = response.data.id
                    this.addInventory(this.product)
                    this.submitted = true
                    this.message = null
                })
                .catch(err => {
                    this.message = err.response.data.message
                })
            },
            newProduct () {
                this.submitted = false
                this.product = {}
            }
        }
    }
</script>