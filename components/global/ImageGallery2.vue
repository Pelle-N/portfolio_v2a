<template>
  <el-carousel :interval="4000" type="card" height="600px">
    <el-carousel-item 
      v-for="(image, index) in galleryImages" 
      :key="index">
      <img :src="image" alt="Gallery image" style="width: 100%; height: 100%; object-fit: cover;" />
    </el-carousel-item>
  </el-carousel>
</template>

<script>
export default {
  data() {
    return {
      galleryImages: [
        '/img/toel 1.jpg',
        '/img/toel 15.jpg',
        '/img/toel 17.jpg',
        '/img/toel 18.jpg',
        '/img/toel 2.jpg',
        '/img/toel 20.jpg',
        '/img/toel 21.jpg',
        '/img/toel 22.jpg',
        '/img/toel 5.jpg',
        '/img/toel 8.jpg',
        '/img/toel 19.jpg'
      ]
    };
  }
};
</script>

<style scoped>
.el-carousel__item img {
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}
</style>
