<script setup>
import { RouterLink, RouterView } from 'vue-router'
import Header from './components/Header.vue'
import { SpeedInsights } from '@vercel/speed-insights/vue';
import { Analytics } from '@vercel/analytics/vue';
</script>

<template>
  <SpeedInsights />
  <div class="min-h-screen flex flex-col bg-base-100">
    <Header />
    <Analytics />
    <RouterView class="flex-grow" />
    <p class="text-xs text-gray-500 text-center p-4 mr-auto">&copy; 2024. 电脑义务维修中心. All rights reserved.</p>
  </div>
</template>
