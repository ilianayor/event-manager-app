<script setup>
import logo from '@/assets/img/eventic-logo.png'
</script>

<template>
  <nav class="bg-[#F0E1D1] border-b border-[#D1B29A]">
    <div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
      <div class="flex h-20 items-center justify-between">
        <div
          class="flex flex-1 items-center justify-center md:items-stretch md:justify-start"
        >
          <!-- Logo -->
          <a class="flex flex-shrink-0 items-center mr-4" href="/">
            <img class="h-40 w-auto md:h-48 lg:h-56" :src="logo" 
              alt="Eventic - актуални събития в София"/>
          </a>
          <div class="md:ml-auto flex items-center">
            <div class="flex space-x-2">
              <a href="/" class="text-black hover:bg-gray-900 hover:text-white rounded-md px-3 py-2">НАЧАЛО</a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>
