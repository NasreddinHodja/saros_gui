<script setup lang="ts">
defineProps<{
  name: string;
  path: string;
}>();
</script>

<template>
  <div class="p-4 flex flex-col items-center justify-around flex- h-[50vh]">
    <div class="w-full h-[90%]">
      <img :src="path" :alt="name" class="w-full h-full object-contain" />
    </div>
    <div class="text-center text-sm mt-2">
      {{ name }}
    </div>
  </div>
</template>
