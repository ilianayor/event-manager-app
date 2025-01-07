<script setup>
import { defineProps, defineEmits } from 'vue';

defineProps({
  event: {
    type: Object,
    required: true
  }
});

defineEmits(['delete-event']);
</script>

<template>
  <div class="bg-white rounded-xl shadow-md relative">
    <div class="p-4">
      <!-- Event Image -->
      <img :src="event.image" :alt="event.title" class="w-full h-48 object-cover rounded-t-xl mb-4" />

      <!-- Event Details -->
      <div class="mb-6">
        <div class="text-gray-600 my-2">{{ event.category }}</div>
        <h3 class="text-xl font-bold">{{ event.title }}</h3>
      </div>

      <div class="mb-5">
        {{ event.description }}
      </div>

      <h3 class="text-gray-600 mb-2">{{ event.date }} </h3>
      <h3 class="text-gray-600 mb-2">Начален час: {{ event.time }} </h3>

      <div class="border border-gray-100 mb-5"></div>

      <div class="flex flex-col lg:flex-row justify-between mb-4">
        <div class="text-gray-600 mb-3">
          <i class="fa-solid fa-location-dot text-lg"></i>
          {{ event.location }}
        </div>
        <div class="flex flex-col gap-3">
        <button class="h-[36px] bg-black hover:bg-gray-700 text-white px-4 py-2 rounded-lg text-center text-sm">
          Научи повече
        </button>
        <button
            @click="$emit('delete-event', event.id)"
            class="h-[36px] bg-red-500 hover:bg-red-700 text-white px-4 py-2 rounded-lg text-center text-sm">
            Изтрий
          </button>
          </div>
      </div>
    </div>
  </div>
</template>
