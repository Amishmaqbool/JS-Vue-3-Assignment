<template>
  <div class="relative">
    <button @click="toggleDropdown" class="px-4 py-2 bg-blue-600 text-white rounded-lg shadow hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-700 focus:ring-opacity-50 transition duration-150 ease-in-out">
      Dropdown
    </button>
    
    <transition name="fade">
      <div v-if="isOpen" class="absolute left-0 mt-1 w-56 rounded-md shadow-lg bg-white z-10">
        <ul class="py-1">
          <li v-for="item in items" :key="item.value" @click="toggleSelection(item)" class="px-4 py-2 hover:bg-gray-100 cursor-pointer transition duration-150 ease-in-out" :class="{ 'bg-blue-200': isSelected(item) }">
            {{ item.title }}
          </li>
        </ul>
      </div>
    </transition>
  </div>
</template>

<script setup>
import { ref, watchEffect } from 'vue';

const props = defineProps({
  items: Array,
  modelValue: Array 
});

const emit = defineEmits(['update:modelValue']);

const isOpen = ref(false);
const selectedItems = ref([...props.modelValue]); 

function toggleDropdown() {
  isOpen.value = !isOpen.value;
}

function toggleSelection(item) {
  const index = selectedItems.value.findIndex(selected => selected.value === item.value);
  if (index > -1) {
 
    selectedItems.value.splice(index, 1);
  } else {
  
    selectedItems.value.push(item);
  }
  emit('update:modelValue', selectedItems.value);
}

function isSelected(item) {
  return selectedItems.value.some(selected => selected.value === item.value);
}

watchEffect(() => {
  if (!props.modelValue.length) {
    selectedItems.value = []; // Reset if the external model is cleared
  }
});
</script>

<style scoped>
/* Tailwind CSS classes handle most of the styling */
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.3s ease;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
</style>
