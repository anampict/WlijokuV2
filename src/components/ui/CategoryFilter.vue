<script setup>
defineProps({
  categories: {
    type: Array,
    default: () => [],
  },
  activeCategory: {
    type: String,
    default: '',
  },
})

defineEmits(['update:activeCategory'])
</script>

<template>
  <div class="flex items-center gap-2">
    <button
      v-for="cat in categories"
      :key="cat"
      @click="$emit('update:activeCategory', cat)"
      class="px-4 py-1.5 rounded-full text-sm font-medium transition-all border"
      :class="
        activeCategory === cat
          ? 'bg-green-800 text-white border-green-800'
          : 'bg-white text-gray-600 border-gray-200 hover:border-gray-400'
      "
    >
      {{ cat }}
    </button>
  </div>
</template>
