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

const submitOrder = async () => {
  if (!form.value.name || !form.value.date || !form.value.main || !form.value.drink || !form.value.side) {
    alert('⚠️ 請完整填寫所有欄位');
    return;
  }

  const url ='https://script.google.com/macros/s/AKfycbzX-POHnPEyoIiTTytuQUFdfq2rwgPATzwUC74ATCXBqlM6SNOvq07B7Ib8DeMFDfVL/exec';

  try {
    const response = await fetch(url, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(form.value),
    });

    const resultText = await response.text();
    console.log('伺服器回應：', resultText);

    if (resultText.includes('success')) {
      alert('✅ 訂單已送出並寫入試算表！');
    } else {
      alert('⚠️ 無法確認是否成功寫入，請查看試算表');
    }
  } catch (error) {
    console.error('❌ 發送失敗：', error);
    alert('❌ 發送失敗，請稍後再試');
  }
};

</script>