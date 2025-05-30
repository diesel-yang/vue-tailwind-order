<template>
  <form @submit.prevent="submitOrder" class="w-full max-w-md bg-white shadow-md rounded px-8 py-6">
    <h2 class="text-2xl font-bold mb-4 text-center">線上訂餐</h2>

    <div class="mb-4">
      <label class="block mb-1 font-medium">姓名：</label>
      <input v-model="form.name" type="text" required class="border p-2 rounded w-full" />
    </div>

    <div class="mb-4">
      <label class="block mb-1 font-medium">用餐日期：</label>
      <input v-model="form.date" type="date" required class="border p-2 rounded w-full" />
    </div>

    <div class="mb-4">
      <label class="block mb-1 font-medium">主餐：</label>
      <select v-model="form.main" required class="border p-2 rounded w-full">
        <option disabled value="">請選擇</option>
        <option v-for="item in mains" :key="item">{{ item }}</option>
      </select>
    </div>

    <div class="mb-4">
      <label class="block mb-1 font-medium">飲品：</label>
      <select v-model="form.drink" required class="border p-2 rounded w-full">
        <option disabled value="">請選擇</option>
        <option v-for="item in drinks" :key="item">{{ item }}</option>
      </select>
    </div>

    <div class="mb-4">
      <label class="block mb-1 font-medium">副餐：</label>
      <select v-model="form.side" required class="border p-2 rounded w-full">
        <option disabled value="">請選擇</option>
        <option v-for="item in sides" :key="item">{{ item }}</option>
      </select>
    </div>

    <div class="mb-6">
      <label class="block mb-1 font-medium">備註：</label>
      <textarea v-model="form.note" rows="2" class="border p-2 rounded w-full"></textarea>
    </div>

    <button type="submit" class="w-full bg-blue-600 text-white px-4 py-2 rounded hover:bg-blue-700">
      送出訂單
    </button>
  </form>
</template>

<script setup>
import { ref } from 'vue'

const form = ref({
  name: '',
  date: '',
  main: '',
  drink: '',
  side: '',
  note: '',
})

const mains = ['鮮蝦蟹醬黃咖哩', '綠咖喱嫩雞', '瑪莎曼牛肋咖哩']
const drinks = ['泰式奶茶', '芒果冰茶', '火烤椰子咖啡']
const sides = ['南薑椰汁雞湯', '茉莉牛奶冰淇淋', '斑蘭葉豆花']

const submitOrder = async () => {
  if (!form.value.name || !form.value.date || !form.value.main || !form.value.drink || !form.value.side) {
    alert('⚠️ 請完整填寫所有欄位');
    return;
  }

  const url = 'https://script.google.com/macros/s/AKfycbx8tHeXW4tFqtRiRuuPus8EGnS_5mWVuPHI952jVZXSVoDZm3jq9USVR---snaz1hkdWg/exec'
  try {
    const response = await fetch(url, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(form.value),
    });

    const resultText = await response.text();
    console.log('伺服器回應：', resultText);
    console.log('送出資料：', form.value);

    alert('✅ 訂單已送出');
  } catch (error) {
    alert('❌ 發送失敗，請稍後再試');
    console.error('錯誤細節：', error);
  }
}
</script>