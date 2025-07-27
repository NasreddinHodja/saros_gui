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

const handleBlur = () => {
  setTimeout(() => {
    if (inputRef.value) {
      inputRef.value.focus();
    }
  }, 20);
};
</script>

<template>
  <div class="flex w-full">
    <span class="font-bold">>&nbsp;</span>
    <input
      ref="input-ref"
      v-model="input"
      @keydown.enter="handleCommand"
      type="text"
      class="w-full font-mono p-0 text-white bg-black outline-none"
      :autofocus="true"
      @blur="handleBlur"
    />
  </div>
</template>
