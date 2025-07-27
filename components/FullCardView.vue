<script setup lang="ts">
const emit = defineEmits<{
  (e: "close"): void;
}>();

defineProps<{
  url: string;
  name: string;
}>();

const img = ref<HTMLImageElement | null>(null);
const isLoading = ref(true);

const handleClose = () => {
  emit("close");
};
</script>

<template>
  <div
    class="absolute top-0 left-0 w-full h-full z-40 bg-black/90 flex flex-col justify-center items-center px-2 py-10 gap-4"
    @click="handleClose"
  >
    <div
      class="absolute top-4 md:top-10 right-4 md:right-10 z-50 text-5xl select-none cursor-pointer text-white"
      @click.stop="handleClose"
    >
      ×
    </div>

    <img
      :src="url"
      @click.stop=""
      class="flex-1 max-w-full object-contain min-h-0"
    />

    <div
      class="text-white text-center max-w-full mt-2 flex-shrink-0 text-wrap break-words"
      @click.stop=""
    >
      {{ name }}
    </div>
  </div>
</template>
