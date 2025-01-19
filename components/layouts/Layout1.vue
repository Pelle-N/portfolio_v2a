<template>
  <div class="layout1">
    <ClientOnly>
      <!-- Drawer menu remains unchanged -->
      <div class="pr-5 z-100">
        <Drawer />
      </div>

      <!-- Main container for portfolio content -->
      <div class="container">
        <!-- Title -->
        <h1 class="text-4xl md:text-5xl lg:text-6xl font-bold mb-4">{{ data.title }}</h1>

        <!-- Subtitle -->
        <h2 class="text-2xl md:text-3xl lg:text-4xl font-semibold text-gray-700 mb-6">{{ data.subtitle }}</h2>

        <!-- Text Introduction -->
        <p class="text-lg md:text-xl lg:text-2xl text-gray-600 leading-relaxed mb-8">
           Communication is key
        </p>

        <!-- Main Text -->
        <div class="prose lg:prose-xl mb-10">
          <ContentRenderer :value="data" />
        </div>

        <!-- Image Gallery Section -->
        <div v-if="data.imagegallery && data.imagegallery.showgallery == true" class="pt-10 pb-20">
          <ImageGallery />
        </div>

        <!-- Footer Section -->
        <div class="text-xs leading-3 container">
          <hr class="my-6">
          <p class="text-xs opacity-50 hover:opacity-100 pb-5">Last update: {{ formatDate(data.date) }}</p>
          <article v-if="data.tags" class="tags">
            <li v-for="(item, index) in data.tags" :key="index" class="pt-2 text-xs opacity-50 hover:opacity-100">
              <NuxtLink :to="`/tags/${item}`">{{ item }}</NuxtLink>
            </li>
          </article>
          <template>
            <UAvatar
            src="https://avatars.githubusercontent.com/u/739984?v=4"
            alt="Avatar"
          />
    </template>
        </div>

        <!-- Social Share Buttons -->
        <ShareButtons />
      </div>

      <!-- SEO Metadata -->
      <Title>{{ data.title }}</Title>
      <Meta name="description" :content="data.description" />
      <Meta name="tags" :content="data.tags" />
      <Meta name="keywords" :content="data.tags.join(', ')" />
      <Meta property="og:title" :content="data.title" />
      <Meta property="og:description" :content="data.description" />
      <Meta property="og:image" :content="data.thumbnail" />
      <Meta property="og:url" :content="data.url" />
      <Meta property="og:type" content="article" />
    </ClientOnly>
  </div>
</template>

<script setup>
defineProps(['data', 'formatDate']);
</script>

<style scoped>
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 15px;
}
.prose {
  font-size: 1rem;
  line-height: 1.75;
  color: #333;
}
</style>
  