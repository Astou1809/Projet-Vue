<template>
  <form class="form" @submit.prevent="submitForm">
    <h2>Ajouter un produit</h2>

    <input
      v-model="form.name"
      placeholder="Nom du produit"
      required
    />

    <select v-model="form.category" required>
      <option value="">Catégorie</option>
      <option
        v-for="cat in categories"
        :key="cat"
        :value="cat"
      >
        {{ cat }}
      </option>
    </select>

    <input
      v-model.number="form.price"
      type="number"
      placeholder="Prix"
      min="0"
      required
    />

    <textarea
      v-model="form.description"
      placeholder="Description"
    ></textarea>

    <button type="submit">Valider</button>
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
        price: 0,
        description: ''
      }
    }
  },
  methods: {
    submitForm() {
      this.$emit('add-product', { ...this.form })
      this.form = {
        name: '',
        category: '',
        price: 0,
        description: ''
      }
    }
  }
}
</script>

<style scoped>
.form {
  background: var(--card-light);
  color: var(--text-light);
  padding: 20px;
  border-radius: 16px;
  max-width: 320px;
  margin: 30px auto;
}

.dark .form {
  background: var(--card-dark);
  color: var(--text-dark);
}

input,
select,
textarea {
  width: 100%;
  margin-bottom: 12px;
  padding: 8px;
  border-radius: 8px;
}

button {
  width: 100%;
  padding: 10px;
}
</style>
