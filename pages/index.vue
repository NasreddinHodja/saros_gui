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
    class="h-full w-full flex flex-col gap-16 items-center justify-center bg-black"
  >
    <div class="flex flex-row gap-4 max-w-full">
      <div v-for="card in drawedCards" :key="card.path">
        <CardDisplay
          :name="card.name"
          :path="card.path"
          class="transition-opacity duration-500 delay-500"
        />
      </div>
    </div>

    <CliTerminal @draw="drawRandomCards" @clear="clearDrawedCards" />
    <img src="@/public/e_logo.jpg" class="w-24 absolute bottom-10 left-10" />
    <img
      src="@/public/seed_logo.png"
      class="w-40 absolute bottom-10 right-10"
    />
  </div>
</template>
