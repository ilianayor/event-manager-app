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

const filteredEvents = computed(() =>
  events.value.filter(
    (event) =>
      event.title.toLowerCase().includes(filter.value.toLowerCase()) ||
      event.category.toLowerCase().includes(filter.value.toLowerCase())
  )
);

const addNewEvent = (newEvent) => {
  events.value.push(newEvent);
  showAddEventForm.value = false;
};

const deleteEvent = (eventId) => {
  events.value = events.value.filter((event) => event.id !== eventId);
};

</script>

<template>
  <Navbar />
  <HeaderComponent />
  <EventFilter v-model="filter" />
  <div class="text-center my-6">
    <button
      @click="showAddEventForm = !showAddEventForm"
      class="bg-black text-white py-2 px-4 rounded-lg hover:bg-gray-700"
    >
      Добави събитие
    </button>
  </div>
  <AddEvent v-if="showAddEventForm" @add-event="addNewEvent" />
  <EventList :events="filteredEvents" @delete-event="deleteEvent"/>
</template>
