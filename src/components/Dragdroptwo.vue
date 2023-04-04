<template>
  <div
    class="dropzone"
    @dragover.prevent
    @dragenter.prevent
    @dragleave.prevent
    @drop.prevent="handleDrop"
  >
    <div>
      <p>Drag and drop files here</p>
    </div>
    <div>
      <p>Drop files here</p>
    </div>
  </div>
</template>

<script setup lang="ts">
function handleDrop(event: any) {
  event.preventDefault();
  const files = Array.from(event.dataTransfer.files);
  // do something with the dropped files
  console.log(files);
}
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
