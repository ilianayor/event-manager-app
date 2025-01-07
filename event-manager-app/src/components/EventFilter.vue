<script setup>
import { ref, defineEmits, defineModel } from 'vue';

const { modelValue } = defineModel({
  modelValue: String,
  default: ''
});

const emit = defineEmits(['update:modelValue']);
const updateFilter = (event) => {
  emit('update:modelValue', event.target.value);
};
</script>

<template>
  <div class="bg-[#F0E1D1] p-4 rounded-xl shadow-md mb-6">
    <input
      v-model="modelValue"
      @input="updateFilter"
      type="text"
      placeholder="Намери събитие по име или категория"
      class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-black"
    />
  </div>
</template>
