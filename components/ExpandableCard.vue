<script setup lang="ts">
defineProps<{
  thumbUrl: string;
  originUrl: string;
  name: string;
}>();

const isExpanded = ref(false);

const expandImage = (e: Event) => {
  isExpanded.value = true;
};

const collapseImage = () => {
  isExpanded.value = false;
};
</script>

<template>
  <div class="flex flex-col px-2 inline-block">
    <div
      @click="expandImage"
      class="flex flex-col cursor-pointer items-center gap-3"
    >
      <div class="overflow-hidden">
        <img :src="thumbUrl" class="bject-cover w-full" />
      </div>
      <div class="text-center text-wrap break-all w-full">
        {{ name }}
      </div>
    </div>
    <FullCardView
      v-if="isExpanded"
      :url="originUrl"
      :name="name"
      @close="collapseImage"
    />
  </div>
</template>
