<template>
  <form class="form">
    <h2>Produit</h2>
    <input placeholder="Nom du produit" />
    <input type="number" placeholder="Prix" />
    <button>Valider</button>
  </form>
</template>

<script>
export default {}
</script>

<style scoped>
.form {
  background: white;
  padding: 20px;
  border-radius: 10px;
  max-width: 300px;
  margin-top: 20px;
}

input {
  width: 100%;
  margin-bottom: 10px;
  padding: 8px;
}

button {
  width: 100%;
  padding: 10px;
}
</style>
