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
const showAddEventForm = ref(false);  // For controlling the modal visibility
const showFilterForm = ref(false);

const filteredEvents = computed(() =>
  events.value.filter(
    (event) =>
      event.title.toLowerCase().includes(filter.value.toLowerCase()) ||
      event.category.toLowerCase().includes(filter.value.toLowerCase())
  )
);

const addNewEvent = (newEvent) => {
  // Add new event to the start of the array using unshift
  events.value.unshift(newEvent);
  showAddEventForm.value = false;  // Close the modal when the event is added
};

const deleteEvent = (eventId) => {
  events.value = events.value.filter((event) => event.id !== eventId);
};
</script>

<template>
  <Navbar />
  <HeaderComponent />

  <!-- Container for both buttons side by side, centered -->
  <div class="flex justify-center space-x-4 my-6">
    <!-- Add Event Button -->
    <button
      @click="showAddEventForm = !showAddEventForm; showFilterForm = false"
      class="bg-black text-white py-2 px-4 rounded-lg hover:bg-gray-700"
    >
      Добави събитие
    </button>

    <!-- Filter Button -->
    <button
      @click="showFilterForm = !showFilterForm; showAddEventForm = false"
      class="bg-black text-white py-2 px-4 rounded-lg hover:bg-gray-700"
    >
      Филтър
    </button>
  </div>

  <!-- Modal to Add Event -->
  <div v-if="showAddEventForm" class="fixed inset-0 bg-gray-500 bg-opacity-50 flex items-center justify-center z-50">
    <div class="bg-white p-6 rounded-lg w-full sm:w-1/2" @click.stop>
      <AddEvent @add-event="addNewEvent" @close-modal="showAddEventForm = false" />
    </div>
  </div>

  <!-- Show the Event Filter if showFilterForm is true -->
  <div v-if="showFilterForm">
    <EventFilter v-model="filter" />
  </div>

  <!-- Event List -->
  <EventList :events="filteredEvents" @delete-event="deleteEvent"/>
</template>
