<template>
  <main>
    <DocxUploader @change="handleFileChange" />
    <DocxViewer :file="docxFile?.raw" />
    <!--    <Editor />-->
  </main>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import Editor from '@/components/TipTapEditor.vue'
import DocxUploader from '@/components/DocxUploader.vue'
import DocxViewer from '@/components/DocxViewer.vue'
import type { UploadUserFile } from 'element-plus'

const docxFile = ref<UploadUserFile | null>(null)

const handleFileChange = (file: UploadUserFile) => {
  console.log('Selected file:', file)
  docxFile.value = file
}
</script>
