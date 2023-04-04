<template>
  <div
    class="dropzone"
    @dragover.prevent
    @dragenter.prevent="isDragging = true"
    @dragleave.prevent="isDragging = false"
    @drop.prevent="handleDrop"
  >
    <div v-if="!isDragging">
      <p>Drag and drop files here</p>
    </div>
    <div v-else>
      <p>Drop files here</p>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const isDragging = ref(false);

    function handleDrop(event) {
      event.preventDefault();
      const files = Array.from(event.dataTransfer.files);
      // do something with the dropped files
      console.log(files);
      isDragging.value = false;
    }

    return { isDragging, handleDrop };
  },
};
</script>

<style scoped>
.dropzone {
  width: 300px;
  height: 200px;
  border: 2px dashed #ccc;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
