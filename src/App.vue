<template>
  <div :class="theme" id="app">

    <!-- Toolbar -->
    <div class="toolbar">
      <button @click="view = 'list'">Liste</button>
      <button @click="view = 'grid'">Grille</button>
      <button @click="view = 'cards'">Cartes</button>
      <button @click="toggleTheme">Changer de thème</button>
    </div>

    <h1>Catalogue de produits</h1>

    <!-- Filtrage -->
    <select v-model="filterCategory">
      <option value="">Toutes catégories</option>
      <option v-for="cat in categories" :key="cat" :value="cat">
        {{ cat }}
      </option>
    </select>

    <!-- Produits -->
    <div :class="view">
      <ProductCard
        v-for="p in filteredProducts"
        :key="p.id"
        :product="p"
        @select="openModal"
        @delete="deleteProduct"
      />
    </div>

    <!-- Modal -->
    <div v-if="selectedProduct" class="modal">
      <div class="modal-content">
        <h2>{{ selectedProduct.name }}</h2>
        <p>{{ selectedProduct.description }}</p>
        <p><strong>{{ selectedProduct.price }} €</strong></p>
        <button @click="selectedProduct = null">Fermer</button>
      </div>
    </div>

    <!-- Formulaire -->
    <ProductForm
      :categories="categories"
      @add-product="addProduct"
    />

  </div>
</template>

<script>
import ProductCard from './components/ProductCard.vue'
import ProductForm from './components/ProductForm.vue'

export default {
  components: { ProductCard, ProductForm },

  data() {
    return {
      view: 'cards',
      theme: 'light',
      selectedProduct: null,
      filterCategory: '',
      categories: [],
      products: []
    }
  },

  mounted() {
    fetch('https://dummyjson.com/products?limit=6')
      .then(res => res.json())
      .then(data => {
        this.products = data.products.map(p => ({
          id: p.id,
          name: p.title,
          price: p.price,
          category: p.category,
          description: p.description,
          image: p.thumbnail,
          promo: p.discountPercentage > 10,
          stock: p.stock
        }))

        this.categories = [...new Set(this.products.map(p => p.category))]
      })
  },

  computed: {
    filteredProducts() {
      if (!this.filterCategory) return this.products
      return this.products.filter(
        p => p.category === this.filterCategory
      )
    }
  },

  methods: {
    openModal(product) {
      this.selectedProduct = product
    },
    toggleTheme() {
      this.theme = this.theme === 'light' ? 'dark' : 'light'
    },
    addProduct(product) {
      product.id = Date.now()
      this.products.push(product)
    },
    deleteProduct(id) {
      this.products = this.products.filter(p => p.id !== id)
    }
  }
}

</script>

<style>
:root {
  --primary: #4f46e5;
}

button {
  background: var(--primary);
}

.light {
  background: #f5f5f5;
  color: #000;
}

.dark {
  background: #1e1e1e;
  color: #fff;
}

.toolbar button {
  margin-right: 5px;
}

.list {
  display: block;
}

.grid,
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}

.modal {
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.6);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background: white;
  padding: 20px;
  border-radius: 10px;
}
</style>
