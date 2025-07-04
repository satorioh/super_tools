<template>
  <main class="home">
    <div class="header">
      <DocxUploader @change="handleFileChange" @remove="handleFileRemove" />
      <DocxViewer :file="docxFile?.raw" />
    </div>
  </main>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import DocxUploader from '@/components/DocxUploader.vue'
import DocxViewer from '@/components/DocxViewer.vue'
import type { UploadUserFile } from 'element-plus'

const docxFile = ref<UploadUserFile | null>(null)

const handleFileChange = (file: UploadUserFile) => {
  docxFile.value = file
}

const handleFileRemove = () => {
  docxFile.value = null
}
</script>

<style lang="scss" scoped>
.home {
  padding: 20px;
  .header {
    display: flex;
    align-items: center;
  }
}
</style>
