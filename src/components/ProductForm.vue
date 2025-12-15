<template>
  <form @submit.prevent="submitForm">
    <input v-model="form.name" placeholder="Nom" required>
    <select v-model="form.category" required>
      <option value="">Catégorie</option>
      <option v-for="cat in categories" :key="cat" :value="cat">{{ cat }}</option>
    </select>
    <input v-model.number="form.price" type="number" placeholder="Prix" required min="0">
    <button type="submit">Ajouter</button>
  </form>
</template>

<script>
export default {
  name: 'ProductForm',
  props: {
    categories: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      form: {
        name: '',
        category: '',
        price: 0
      }
    }
  },
  methods: {
    submitForm() {
      if (this.form.name && this.form.category && this.form.price > 0) {
        this.$emit('add-product', { ...this.form });
        this.form = { name: '', category: '', price: 0 };
      }
    }
  }
}
</script>

<style scoped>
form {
  margin-bottom: 20px;
}

input, select, button {
  margin: 5px;
  padding: 5px;
}
</style>