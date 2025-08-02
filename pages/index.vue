<script setup lang="ts">
import cardsData from "@/utils/cards.json";

const drawedCards = ref<{ name: string; path: string }[]>([]);

const drawRandomCards = (count: number) => {
  drawedCards.value = cardsData.sort(() => Math.random() - 0.5).slice(0, count);
};

const clearDrawedCards = () => {
  drawedCards.value = [];
};
</script>

<template>
  <div
    class="min-h-full w-full flex flex-col items-center bg-black overflow-y-auto"
  >
    <div
      class="flex-1 flex flex-col gap-14 items-center md:justify-center w-full"
    >
      <DrawedCardList :drawedCards="drawedCards" class="mt-10" />
      <CliTerminal
        @draw="drawRandomCards"
        @clear="clearDrawedCards"
        class="mb-32"
      />
    </div>
  </div>
</template>
