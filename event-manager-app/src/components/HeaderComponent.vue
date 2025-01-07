<script setup>
import { defineProps } from 'vue';

defineProps({
    title: {
        type: String,
        default: 'Събития в София'
    },
    subtitle: {
        type: String,
        default: 'Открийте най-интересните събития в столицата'
    }
})
</script>

<template>
  <section class="bg-white py-5 mb-4">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 flex flex-col items-center">
      <div class="text-center">
        <h1 class="text-4xl font-extrabold text-black sm:text-5xl md:text-5xl">
          {{ title }}
        </h1>
        <p class="my-4 text-xl text-black">
          {{ subtitle }}
        </p>
      </div>
    </div>
  </section>
</template>
