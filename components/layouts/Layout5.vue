<template>
  <div class="about-page bg-gray-50 min-h-screen flex flex-col">
    <!-- Hero Section -->
    <header class="bg-pink-500 text-white py-10">
      <div class="container mx-auto text-center">
        <h1 class="text-4xl font-bold">{{ data.title }}</h1>
      </div>
    </header>

     <!-- Drawer and navigation -->
     <div class="absolute top-0 right-0 z-10 pr-5">
        <Drawer/> 
      </div>

    <!-- About Section -->
    <section class="container mx-auto px-4 py-10">
      <div class="grid grid-cols-1 md:grid-cols-2 gap-8 items-center">
        <!-- Image Placeholder -->
        <div>
          <img
            :src="data.thumbnail || '/placeholder.jpg'"
            alt="About me image"
            class="h-90"
          />
        </div>

        <!-- About Text -->
        <div>
          <h2 class="text-3xl font-bold mb-4">Hey, Ik ben Pelle </h2>
          <p class="text-lg text-gray-700 leading-relaxed mb-4">
            {{ data.description }}
          </p>
        </div>
      </div>
    </section>

    <!-- Contact Form Section -->
    <section class="bg-white py-10">
      <div class="container mx-auto px-4">
        <h2 class="text-2xl font-bold text-center mb-6 text-pink-500">Contact Me</h2>
        <form
          @submit.prevent="submitForm"
          class="max-w-lg mx-auto bg-gray-100 shadow-md rounded-lg p-6"
        >
          <div class="mb-4">
            <label for="name" class="block text-gray-700 font-bold mb-2">Your Name</label>
            <input
              id="name"
              v-model="formData.name"
              type="text"
              class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-pink-500"
              required
            />
          </div>
          <div class="mb-4">
            <label for="email" class="block text-gray-700 font-bold mb-2">Your Email</label>
            <input
              id="email"
              v-model="formData.email"
              type="email"
              class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-pink-500"
              required
            />
          </div>
          <div class="mb-4">
            <label for="message" class="block text-gray-700 font-bold mb-2">Your Message</label>
            <textarea
              id="message"
              v-model="formData.message"
              rows="4"
              class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-pink-500"
              required
            ></textarea>
          </div>
          <button
            type="submit"
            class="w-full bg-pink-500 text-white py-2 rounded-lg hover:bg-pink-800 focus:outline-none focus:ring-2 focus:ring-pink-500"
          >
            Send Message
          </button>
        </form>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  props: ["data"], // Assuming data is passed from the markdown file
  data() {
    return {
      formData: {
        name: "",
        email: "",
        message: "",
      },
    };
  },
  methods: {
    submitForm() {
      // Simple form submission logic; replace with actual email handling
      alert(`Thanks, ${this.formData.name}! Your message has been sent.`);
      this.formData = { name: "", email: "", message: "" };
    },
  },
};
</script>

<style scoped>
/* You can add any additional styles if needed */
</style>
