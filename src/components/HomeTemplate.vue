<template>
  <v-carousel height="619" cycle show-arrows="hover">
    <v-carousel-item v-for="item in items" :src="item" cover></v-carousel-item>
  </v-carousel>
</template>

<script lang="ts" setup>
import { ref } from "vue";
const items = ref([
  "src/assets/image-1.jpg",
  "src/assets/image-2.jpg",
]);
</script>
