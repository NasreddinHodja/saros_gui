<script setup lang="ts">
const emit = defineEmits<{
  (event: "command", command: string): void;
}>();

const input = ref("");
const inputRef = useTemplateRef("input-ref");

defineExpose({ inputRef });

const handleCommand = () => {
  emit("command", input.value);
  input.value = "";
};
</script>

<template>
  <div class="flex w-full">
    <span>>&nbsp;</span>
    <input
      ref="input-ref"
      v-model="input"
      @keydown.enter="handleCommand"
      type="text"
      class="w-full font-mono p-0 text-white bg-black outline-none"
      :autofocus="true"
    />
  </div>
</template>
