<template>
  <div class="min-h-screen bg-orange-50 text-gray-900">
    <header class="bg-orange-500 text-white p-4 text-center text-xl font-bold">
      山色｜預先點餐
    </header>
    <main class="py-8 px-4">
      <OrderForm />
    </main>
  </div>
</template>

<script setup>
import OrderForm from './components/OrderForm.vue'
</script>