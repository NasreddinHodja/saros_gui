<script setup lang="ts">
useHead({
  titleTemplate: (titleChunk) =>
    titleChunk ? `${titleChunk} - S.E.E.D. SAROS` : "S.E.E.D. SAROS",
  meta: [
    { property: "og:title", content: "S.E.E.D. SAROS" },
    { property: "og:description", content: "S.E.E.D. Tarot Bot" },
    { property: "og:image", content: "/seed_logo.png" },
    { property: "og:type", content: "website" },
    { name: "twitter:card", content: "summary_large_image" },
    { name: "twitter:image", content: "/seed_logo.png" },
  ],
  link: [{ rel: "icon", type: "image/x-icon", href: "/favicon.ico" }],
});
</script>

<template>
  <div
    class="h-screen w-screen flex flex-col bg-black text-white font-mono overflow-hidden"
  >
    <NuxtPage />

    <div
      class="w-full fixed bottom-0 left-0 bg-black z-10 flex justify-between items-center pb-6 pt-4 px-6"
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
