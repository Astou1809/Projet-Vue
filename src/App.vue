<template>
  <div :class="theme" id="app">
    <!-- Boutons affichage -->
    <div class="toolbar">
      <button @click="view = 'list'">Liste</button>
      <button @click="view = 'grid'">Grille</button>
      <button @click="view = 'cards'">Cartes</button>
      <button @click="toggleTheme">Changer de thème</button>
    </div>

    <h1>Catalogue de produits</h1>

    <!-- Produits -->
    <div :class="view">
      <ProductCard
        v-for="p in products"
        :key="p.id"
        :product="p"
        @select="openModal(p)"
      />
    </div>

    <!-- Modal -->
    <div v-if="selectedProduct" class="modal">
      <div class="modal-content">
        <h2>{{ selectedProduct.name }}</h2>
        <p>{{ selectedProduct.description }}</p>
        <button @click="selectedProduct = null">Fermer</button>
      </div>
    </div>

    <!-- Formulaire -->
    <ProductForm />
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
      products: [
        {
          id: 1,
          name: 'Test du produit',
          price: 99,
          promo: true,
          stock: 10,
          image: 'https://via.placeholder.com/300',
          description: 'Ceci est un produit de démonstration'
        }
      ]
    }
  },

  methods: {
    openModal(product) {
      this.selectedProduct = product
    },
    toggleTheme() {
      this.theme = this.theme === 'light' ? 'dark' : 'light'
    }
  }
}
</script>

<style>
/* Thèmes */
.light {
  background: #f5f5f5;
  color: #000;
}

.dark {
  background: #1e1e1e;
  color: #fff;
}

/* Toolbar */
.toolbar button {
  margin-right: 5px;
}

/* Affichages */
.list {
  display: block;
}

.grid,
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}

/* Modal */
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,0.6);
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal-content {
  background: white;
  padding: 20px;
  border-radius: 10px;
}
</style>
