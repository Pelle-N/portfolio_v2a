<template>
  <div>
    <div v-for="(posts, folderName) in folders" :key="folderName">
      <ul>
        <li v-for="post in posts" :key="post.slug" class="pb-1 md:pb-2 lg:pb-3">
          <NuxtLink
            :to="post._path"
            class="font-bold text-xl lg:text-3xl xl:text-4xl text-pink-500 md:text-blue-900 animate-fade animate-once"
            :class="{ 'animate-ping': animateStates[post.slug] }"
             @click.prevent="triggerAnimationAndNavigate(post.slug, post._path)"
          >
            {{ post.title }}
          </NuxtLink>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useAsyncData, useRouter } from '#app'; // Import router for navigation
import menus from '../../../public/_data/menus.json'; // Import menus.json

// Define a ref for storing grouped and sorted folders
const folders = ref({});
const animateStates = ref({});
const router = useRouter(); // Use router for navigation

// Trigger animation and delay navigation
const triggerAnimationAndNavigate = (slug, path) => {
  // Reset animation state for the post
  animateStates.value[slug] = false;

  setTimeout(() => {
    // Trigger the animation
    animateStates.value[slug] = true;

    // After the animation completes, navigate to the new page
    setTimeout(() => {
      router.push(path);
    }, 30); // Adjust to match the animation duration
  }, 10); // Tiny delay to ensure the animation resets
};

// Fetch folders/posts using Nuxt's content query
const { data: foldersPosts } = await useAsyncData('folders', () =>
  queryContent('/')
    .sort({ numbernavigation: -1 }) // Sorting in descending order (highest first)
    .find()
);

onMounted(() => {
  // Filter and group posts
  let filteredPosts = (foldersPosts.value || []).filter(post => post._dir !== 'tags' && post.numbernavigation !== 0);

  filteredPosts = filteredPosts.filter(post => {
    const folderName = post._dir;

    if (folderName === 'collections' && menus.submenu['excludefromnavigation'] === 2) {
      return false; // Exclude 'collections' folder
    }

    if (menus.submenu['excludefromnavigation'] === 2) {
      return false; // Exclude based on the position value
    }

    return true; // Include other folders
  });

  const grouped = filteredPosts.reduce((acc, post) => {
    const folderName = post._dir; // Folder name is stored in _dir
    if (!acc[folderName]) {
      acc[folderName] = [];
    }
    acc[folderName].push(post);
    return acc;
  }, {});

  // Sort posts within each folder by 'numbernavigation' in descending order
  for (const folder in grouped) {
    grouped[folder].sort((a, b) => b.numbernavigation - a.numbernavigation);
  }

  folders.value = grouped;
});
</script>