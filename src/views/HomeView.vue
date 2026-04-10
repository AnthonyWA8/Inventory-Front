<script setup>
import { ref, onMounted } from 'vue'

const products = ref([])

// 👇 URL de tu backend (Railway)
const url = "https://inventory-back-production-45d2.up.railway.app"

onMounted(async () => {
  try {
    const res = await fetch(`${url}/products`)
    const data = await res.json()
    products.value = data
  } catch (error) {
    console.error("Error cargando productos:", error)
  }
})
</script>

<template>
  <main>
    <h1>Productos</h1>

    <div v-if="products.length === 0">
      No hay productos
    </div>

    <div v-else>
      <div v-for="p in products" :key="p.sku">
        {{ p.name }}
      </div>
    </div>
  </main>
</template>
