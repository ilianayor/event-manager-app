<script setup>
import { ref, defineEmits } from 'vue';

const emit = defineEmits(['add-event', 'close-modal']);

const newEvent = ref({
  title: '',
  image: '',
  category: '',
  description: '',
  date: '',
  time: '',
  location: '',
});

// Define possible categories
const categories = ref([
  'Концерт',
  'Кулинарно събитие',
  'Изложба',
  'Театър',
  'Фестивал',
  'Спортно събитие',
  'Конференция'
]);

const handleSubmit = () => {
  if (
    newEvent.value.title &&
    newEvent.value.image &&
    newEvent.value.category &&
    newEvent.value.description &&
    newEvent.value.date &&
    newEvent.value.time &&
    newEvent.value.location
  ) {
    emit('add-event', { ...newEvent.value });
    resetForm();
  } else {
    alert('Попълнете всички полета!');
  }
};

const resetForm = () => {
  newEvent.value = {
    title: '',
    image: '',
    category: '',
    description: '',
    date: '',
    time: '',
    location: '',
  };
};

const closeModal = () => {
  emit('close-modal');
};
</script>

<template>
  <div class="w-full max-w-4xl mx-auto p-6">
    <h2 class="text-xl font-bold mb-4">Добави ново събитие</h2>
    <form @submit.prevent="handleSubmit" class="space-y-4">
      <input
        v-model="newEvent.title"
        type="text"
        placeholder="Име"
        class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-black"
      />
      <input
        v-model="newEvent.image"
        type="text"
        placeholder="URL адрес на изображение"
        class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-black"
      />
      
      <!-- Category Dropdown -->
      <select
        v-model="newEvent.category"
        class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-black"
      >
        <option value="" disabled>Изберете категория</option>
        <option v-for="category in categories" :key="category" :value="category">
          {{ category }}
        </option>
      </select>
      
      <textarea
        v-model="newEvent.description"
        placeholder="Описание"
        rows="3"
        class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-black"
      ></textarea>
      <input
        v-model="newEvent.date"
        type="date"
        class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-black"
      />
      <input
        v-model="newEvent.time"
        type="time"
        class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-black"
      />
      <input
        v-model="newEvent.location"
        type="text"
        placeholder="Локация"
        class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-black"
      />
      <button
        type="submit"
        class="w-full bg-black text-white py-3 rounded-lg hover:bg-gray-700"
      >
        Добави
      </button>
    </form>
    <button
      @click="closeModal"
      class="w-full bg-gray-500 text-white py-2 rounded-lg mt-4 hover:bg-gray-700"
    >
      Затвори
    </button>
  </div>
</template>

