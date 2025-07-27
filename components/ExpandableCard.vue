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
  <div>
    <div @click="expandImage">
      <img :src="thumbUrl" />
      {{ name }}
    </div>
    <FullCardView
      v-if="isExpanded"
      :url="originUrl"
      :name="name"
      @close="collapseImage"
    />
  </div>
</template>
