<script setup>
import { defineProps, defineEmits } from 'vue';
import EventCard from './EventCard.vue';

defineProps({
  events: {
    type: Array,
    required: true
  }
});

defineEmits(['delete-event']);
</script>

<template>
  <section class="bg-[#F0E1D1] px-4 py-10">
    <div class="container-xl lg:container m-auto">
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <!-- Loop through the events and display each one using EventCard -->
        <EventCard 
          v-for="event in events"
          :key="event.id"
          :event="event" 
          @delete-event="$emit('delete-event', $event)"/>
      </div>
    </div>
  </section>
</template>
