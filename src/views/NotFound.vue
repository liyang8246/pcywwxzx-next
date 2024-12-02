<script setup>
import { onMounted } from 'vue';
import { useRouter } from 'vue-router';

const router = useRouter();

onMounted(() => {
  setTimeout(() => {
    router.push({ path: '/' });
  }, 5000);
});
</script>

<template>
  <div class="grid min-h-full place-content-center px-4">
    <h1 class="uppercase tracking-widest text-base-content">404 | Not Found</h1>
    <h1 class="tracking-widest text-base-content text-sm mx-auto mt-2">Go home in 5 sec</h1>
  </div>
</template>
