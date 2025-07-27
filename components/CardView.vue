<script setup lang="ts">
defineProps<{
  name: string;
  path: string;
}>();
</script>

<template>
  <div
    class="p-4 w-[45vh] md:w-[26vh] flex flex-col items-center justify-around"
  >
    <div class="flex h-full w-full flex-col gap-4">
      <div class="w-full h-[380px]">
        <img :src="path" :alt="name" class="w-full h-full object-fill" />
      </div>
      <div
        class="flex justify-center items-center text-center text-base mt-2 font-bold text-white"
      >
        {{ name }}
      </div>
    </div>
  </div>
</template>
