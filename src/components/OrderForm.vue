<template>
  <form @submit.prevent="submitOrder" class="max-w-lg mx-auto p-6 bg-white rounded shadow">
    <div class="space-y-4">
      <div>
        <label>姓名：</label>
        <input v-model="form.name" type="text" required class="border p-2 rounded w-full" />
      </div>
      <div>
        <label>用餐日期：</label>
        <input v-model="form.date" type="date" required class="border p-2 rounded w-full" />
      </div>
      <div>
        <label>主餐：</label>
        <select v-model="form.main" required class="border p-2 rounded w-full">
          <option disabled value="">請選擇</option>
          <option v-for="item in mains" :key="item">{{ item }}</option>
        </select>
      </div>
      <div>
        <label>飲品：</label>
        <select v-model="form.drink" required class="border p-2 rounded w-full">
          <option disabled value="">請選擇</option>
          <option v-for="item in drinks" :key="item">{{ item }}</option>
        </select>
      </div>
      <div>
        <label>副餐：</label>
        <select v-model="form.side" required class="border p-2 rounded w-full">
          <option disabled value="">請選擇</option>
          <option v-for="item in sides" :key="item">{{ item }}</option>
        </select>
      </div>
      <div>
        <label>備註：</label>
        <textarea v-model="form.note" rows="2" class="border p-2 rounded w-full"></textarea>
      </div>
      <button type="submit" class="bg-orange-500 text-white px-4 py-2 rounded hover:bg-orange-600">
        送出訂單
      </button>
    </div>
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
  const url = 'https://script.google.com/macros/s/AKfycbx8tHeXW4tFqtRiRuuPus8EGnS_5mWVuPHI952jVZXSVoDZm3jq9USVR---snaz1hkdWg/exec'

  if (!form.value.name || !form.value.date || !form.value.main || !form.value.drink || !form.value.side) {
    alert('⚠️ 請完整填寫所有欄位');
    return;
  }

  try {
    await fetch(url, {
      method: 'POST',
      mode: 'no-cors',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(form.value),
    });
    alert('✅ 訂單已送出（系統不回傳結果）');
  } catch (error) {
    alert('❌ 發送失敗，請稍後再試');
    console.error('錯誤細節：', error);
  }
};const submitOrder = async () => {
  const url = 'https://script.google.com/macros/s/AKfycbx8tHeXW4tFqtRiRuuPus8EGnS_5mWVuPHI952jVZXSVoDZm3jq9USVR---snaz1hkdWg/exec';

  // 檢查欄位
  if (!form.value.name || !form.value.date || !form.value.main || !form.value.drink || !form.value.side) {
    alert('⚠️ 請完整填寫所有欄位');
    return;
  }

  try {
    await fetch(url, {
      method: 'POST',
      mode: 'no-cors', // ⚠️ 避免 CORS 問題（但無法讀取回應）
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(form.value),
    });

    alert('✅ 訂單已送出！'); // 若沒錯就是成功
  } catch (error) {
    alert('❌ 發送失敗，請稍後再試');
    console.error('錯誤細節：', error);
  }
};

</script>