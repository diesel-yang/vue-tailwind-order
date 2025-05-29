<template>
  <div class="max-w-2xl mx-auto p-4 space-y-6">
    <h2 class="text-2xl font-bold text-center">山色 Shān Sè 預先點餐</h2>

    <!-- 用餐資訊 -->
    <div class="space-y-2">
      <label class="block font-semibold">用餐人數</label>
      <select v-model="people" class="w-full border p-2 rounded">
        <option disabled value="">請選擇</option>
        <option v-for="n in 6" :key="n" :value="n">{{ n }} 位</option>
      </select>
    </div>

    <div class="space-y-2">
      <label class="block font-semibold">用餐日期</label>
      <input type="date" v-model="date" class="w-full border p-2 rounded" />
    </div>

    <div class="space-y-2">
      <label class="block font-semibold">用餐時段</label>
      <select v-model="time" class="w-full border p-2 rounded">
        <option disabled value="">請選擇</option>
        <option>11:30–13:00</option>
        <option>12:20–13:50</option>
        <option>13:10–14:40</option>
        <option>14:00–15:30</option>
      </select>
    </div>

    <button @click="submit" class="w-full bg-indigo-600 text-white py-2 rounded hover:bg-indigo-700">
      提交訂單
    </button>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const people = ref('')
const date = ref('')
const time = ref('')

const submit = () => {
  alert(`人數：${people.value}, 日期：${date.value}, 時段：${time.value}`)
}
</script>
