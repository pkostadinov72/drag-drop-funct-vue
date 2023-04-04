<template>
  <div class="input-div" @drop.prevent="handleDrop">
    <input type="file" multiple @change="handleFileSelect" />
    <output v-html="imagesArray"></output>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

const imagesArray = ref<File[]>([]);
const images = ref("");

function handleFileSelect(event: any) {
  const files = (event.target as HTMLInputElement).files;
  if (files) {
    for (let i = 0; i < files.length; i++) {
      imagesArray.value.push(files[i]);
    }
    displayImages();
  }
}

function handleDrop(event: DragEvent) {
  event.preventDefault();
  const files = event.dataTransfer?.files;
  if (files) {
    for (let i = 0; i < files.length; i++) {
      if (!files[i].type.match("image")) continue;

      if (imagesArray.value.every((image) => image.name !== files[i].name)) {
        imagesArray.value.push(files[i]);
      }
    }
    displayImages();
  }
}

function displayImages() {
  let images = "";
  imagesArray.value.forEach((image, index) => {
    images += `
      <div class="image">
        <img src="${URL.createObjectURL(image)}" alt="image">
        <span @click="() => deleteImage(${index})">&times;</span>
      </div>
    `;
  });
  images = images; // Assign the updated HTML string to the `images` variable
}
</script>
