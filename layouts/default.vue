<script setup lang="ts">
useHead({
  titleTemplate: (titleChunk) =>
    titleChunk ? `${titleChunk} - S.E.E.D.` : "S.E.E.D.",
  meta: [
    { property: "og:title", content: "S.E.E.D. SAROS" },
    { property: "og:description", content: "S.E.E.D. Tarot Bot" },
    { property: "og:image", content: "/seed_logo.png" },
    { property: "og:type", content: "website" },
    { name: "twitter:card", content: "summary_large_image" },
    { name: "twitter:image", content: "/seed_logo.png" },
  ],
});
</script>

<template>
  <div
    class="h-screen w-screen flex flex-col bg-black text-white font-mono overflow-hidden"
  >
    <NuxtPage />
  </div>
</template>
