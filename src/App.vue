<template>
  <div class="container mx-auto p-8 min-h-[400px] mt-32 max-w-2xl bg-white shadow-md rounded-md">
  <div class="grid grid-cols-2">
      <div class="mt-4">
      <Dropdown :items="dropdownItems" v-model="selectedItems" />
    </div>
    <div class="mt-4 bg-slate-100 px-2 rounded-md">
      <p class="text-lg font-semibold mb-2">Selected items</p>
      <ul class="list-disc pl-4">
        <li v-for="(item, index) in selectedItems" :key="index" class="mb-1">
          {{ item.title }}
        </li>
      </ul>
    </div>
  </div>
  </div>
</template>
<script setup>
import { ref, computed } from 'vue'
import Dropdown from '../components/common/DropDown.vue'

const dropdownItems = [
  { title: 'Electronics', value: 1 },
  { title: 'Clothing', value: 2 },
  { title: 'Home & Garden', value: 3 },
  { title: 'Books', value: 4 },
  { title: 'Sports & Outdoors', value: 5 },
  { title: 'Beauty', value: 6 },
  { title: 'Toys & Games', value: 7 },
  { title: 'Food & Drink', value: 8 },
  { title: 'Health & Wellness', value: 9 },
  { title: 'Automotive', value: 10 },
  { title: 'Furniture', value: 11 },
  { title: 'Art & Collectibles', value: 12 },
  { title: 'Office Supplies', value: 13 },
  { title: 'Crafts & Hobbies', value: 14 },
  { title: 'Pet Supplies', value: 15 }
]

const selectedItems = ref([])

const selectedItemsTitles = computed(() => {
  return selectedItems.value.map(item => item.title);
})
</script>

