<template>
  <main>
    <DocxUploader @change="handleFileChange" />
    <DocxViewer :file="docxFile?.raw" />
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
</script>
