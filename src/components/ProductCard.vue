<template>
  <div
    class="card"
    :class="{ promo: product.promo, out: product.stock === 0 }"
    @click="$emit('select', product)"
  >
    <img :src="product.image" alt="image produit" />

    <h3>{{ product.name }}</h3>
    <p>{{ product.price }} €</p>

    <span v-if="product.promo" class="badge">Promo</span>
    <span v-if="product.stock === 0" class="badge out-badge">Rupture</span>

    <button class="delete" @click.stop="$emit('delete', product.id)">
      Supprimer
    </button>
  </div>
</template>

<script>
export default {
  name: 'ProductCard',
  props: {
    product: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped>
.card {
  background: #ffffff;
  padding: 16px;
  border-radius: 16px;
  box-shadow: 0 8px 20px rgba(0,0,0,0.08);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.card:hover {
  transform: translateY(-4px);
  box-shadow: 0 12px 30px rgba(0,0,0,0.15);
}

button {
  background: #2c3e50;
  color: white;
  border: none;
  border-radius: 10px;
}



.card img {
  width: 100%;
  border-radius: 8px;
}

.promo {
  border: 2px solid red;
}

.out {
  opacity: 0.5;
}

.badge {
  display: inline-block;
  margin-top: 5px;
  padding: 4px 8px;
  background: red;
  color: white;
  border-radius: 5px;
}

.out-badge {
  background: gray;
}

.delete {
  margin-top: 10px;
  width: 100%;
  background: #444;
  color: white;
  border: none;
  padding: 6px;
  border-radius: 5px;
  cursor: pointer;
}
</style>
