<template>
  <li>
    {{ product.name }} - {{ product.category }} - {{ product.price }}€
    <button @click="deleteProduct">Supprimer</button>
  </li>
</template>

<script>
export default {
  name: 'ProductItem',
  props: {
    product: {
      type: Object,
      required: true
    }
  },
  methods: {
    deleteProduct() {
      this.$emit('delete-product', this.product.id);
    }
  }
}
</script>

<style scoped>
li {
  margin: 10px 0;
  padding: 10px;
  border: 1px solid #ccc;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
</style>