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
    class="h-full w-full flex flex-col gap-16 items-center md:justify-center bg-black pt-10 overflow-y-scroll"
  >
    <div class="flex flex-col md:flex-row gap-4 max-w-full">
      <div v-for="card in drawedCards" :key="card.path">
        <CardDisplay
          :name="card.name"
          :path="card.path"
          class="transition-opacity duration-500 delay-500"
        />
      </div>
    </div>

    <CliTerminal
      @draw="drawRandomCards"
      @clear="clearDrawedCards"
      class="mb-28"
    />
    <div
      class="w-full fixed bottom-0 left-0 bg-black z-50 flex justify-between items-center pb-6 pt-4 px-6"
    >
      <a href="https://seed.computer" target="_blank" rel="noopener noreferrer">
        <img src="@/public/e_logo.jpg" class="w-24" />
      </a>
      <a href="https://seed.computer" target="_blank" rel="noopener noreferrer">
        <img src="@/public/seed_logo.png" class="w-40" />
      </a>
    </div>
  </div>
</template>
