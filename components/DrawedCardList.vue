<script setup lang="ts">
defineProps<{
  drawedCards: { name: string; path: string }[];
}>();
</script>

<template>
  <div
    class="flex flex-col md:flex-row gap-x-10 md:gap-x-4 gap-y-10 md:gap-y-4 max-w-full flex-wrap justify-center"
  >
    <ExpandableCard
      v-for="card in drawedCards"
      :key="card.path"
      :name="card.name"
      :originUrl="card.path"
      :thumbUrl="card.path"
      class="md:w-[200px]"
    />
  </div>
</template>
