<script setup>
import Navbar from '@/components/Navbar.vue';
import HeaderComponent from '@/components/HeaderComponent.vue';
import EventFilter from '@/components/EventFilter.vue';
import EventList from '@/components/EventList.vue';
import AddEvent from '@/components/AddEvent.vue';
import eventInfo from '@/events.json'  
import { ref, computed } from 'vue';

const events = ref(eventInfo);
const filter = ref('');
const showAddEventForm = ref(false); 
const showFilterForm = ref(false);

const filteredEvents = computed(() =>
  events.value.filter(
    (event) =>
      event.title.toLowerCase().includes(filter.value.toLowerCase()) ||
      event.category.toLowerCase().includes(filter.value.toLowerCase())
  )
);

const addNewEvent = (newEvent) => {
  events.value.unshift(newEvent);
  showAddEventForm.value = false;  
};

const deleteEvent = (eventId) => {
  events.value = events.value.filter((event) => event.id !== eventId);
};
</script>

<template>
  <Navbar />
  <HeaderComponent />

  <div class="flex justify-center space-x-4 my-6">
    <button
      @click="showAddEventForm = !showAddEventForm; showFilterForm = false"
      class="bg-black text-white py-2 px-4 rounded-lg hover:bg-gray-700"
    >
      Добави събитие
    </button>

    <button
      @click="showFilterForm = !showFilterForm; showAddEventForm = false"
      class="bg-black text-white py-2 px-4 rounded-lg hover:bg-gray-700"
    >
      Филтър
    </button>
  </div>

  <div v-if="showAddEventForm" class="fixed inset-0 bg-gray-500 bg-opacity-50 flex items-center justify-center z-50">
    <div class="bg-white p-6 rounded-lg w-full sm:w-1/2" @click.stop>
      <AddEvent @add-event="addNewEvent" @close-modal="showAddEventForm = false" />
    </div>
  </div>

  <div v-if="showFilterForm">
    <EventFilter v-model="filter" />
  </div>

  <EventList :events="filteredEvents" @delete-event="deleteEvent"/>
</template>
