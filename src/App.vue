<template>
  <div id="app">
    <h1>Gestion des Produits</h1>

    <!-- Formulaire d'ajout -->
    <ProductForm @add-product="addProduct" :categories="categories" />

    <!-- Filtrage -->
    <div>
      <select v-model="filterCategory">
        <option value="">Toutes catégories</option>
        <option v-for="cat in categories" :key="cat" :value="cat">{{ cat }}</option>
      </select>
      <label><input type="checkbox" v-model="showExpensive"> Prix > 100</label>
    </div>

    <!-- Liste des produits -->
    <ul>
      <ProductItem
        v-for="product in filteredProducts"
        :key="product.id"
        :product="product"
        @delete-product="deleteProduct"
      />
    </ul>
  </div>
</template>

<script>
import ProductForm from './components/ProductForm.vue'
import ProductItem from './components/ProductItem.vue'

export default {
  name: 'App',
  components: {
    ProductForm,
    ProductItem
  },
  data() {
    return {
      products: [
        { id: 1, name: 'Ordinateur', category: 'Electronics', price: 1200 },
        { id: 2, name: 'T-shirt', category: 'Clothing', price: 20 },
        { id: 3, name: 'Livre', category: 'Books', price: 15 },
        { id: 4, name: 'Téléphone', category: 'Electronics', price: 800 },
      ],
      categories: ['Electronics', 'Clothing', 'Books'],
      filterCategory: '',
      showExpensive: false,
      nextId: 5
    }
  },
  computed: {
    filteredProducts() {
      let filtered = this.products;
      if (this.filterCategory) {
        filtered = filtered.filter(p => p.category === this.filterCategory);
      }
      if (this.showExpensive) {
        filtered = filtered.filter(p => p.price > 100);
      }
      return filtered;
    }
  },
  methods: {
    addProduct(product) {
      product.id = this.nextId++;
      this.products.push(product);
    },
    deleteProduct(id) {
      this.products = this.products.filter(p => p.id !== id);
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  margin: 20px;
}

ul {
  list-style: none;
  padding: 0;
}
</style>
