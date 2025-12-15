<template>
  <div
    class="card"
    :class="{ promo: product.promo, out: product.stock === 0 }"
    @click="$emit('select')"
  >
    <img :src="product.image" />

    <h3>{{ product.name }}</h3>
    <p>{{ product.price }} €</p>

    <span v-if="product.promo" class="badge">Promo</span>
    <span v-if="product.stock === 0" class="badge out-badge">Rupture</span>
  </div>
</template>

<script>
export default {
  props: {
    product: Object
  }
}
</script>

<style scoped>
.card {
  background: white;
  padding: 15px;
  border-radius: 12px;
  cursor: pointer;
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
</style>
