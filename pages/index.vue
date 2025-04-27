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
    class="h-full w-full flex flex-col gap-4 items-center justify-center bg-black"
  >
    <div class="flex flex-row space-x-4">
      <div
        v-for="card in drawedCards"
        :key="card.path"
        class="flex-shrink-0 flex-grow-0 basis-1/5"
        :style="{
          flexBasis:
            drawedCards.length === 1
              ? '100%'
              : drawedCards.length === 2
              ? '50%'
              : drawedCards.length === 3
              ? '33%'
              : drawedCards.length === 4
              ? '25%'
              : '20%',
        }"
      >
        <CardDisplay
          :name="card.name"
          :path="card.path"
          class="transition-opacity duration-500 delay-500"
        />
      </div>
    </div>

    <CliTerminal @draw="drawRandomCards" @clear="clearDrawedCards" />
  </div>
</template>
