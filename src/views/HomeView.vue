<template>
  <main class="home">
    <div class="header">
      <DocxUploader @change="handleFileChange" @remove="handleFileRemove" />
      <DocxViewer :file="docxFile?.raw" />
    </div>
    <div class="content">
      <DocxConvert :file="docxFile?.raw" @converted="handleConverted" />
      <Editor v-model="htmlContent" />
    </div>
  </main>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import DocxUploader from '@/components/DocxUploader.vue'
import DocxViewer from '@/components/DocxViewer.vue'
import DocxConvert from '@/components/DocxConvert.vue'
import Editor from '@/components/TipTapEditor.vue'
import type { UploadUserFile } from 'element-plus'

const docxFile = ref<UploadUserFile | null>(null)
const htmlContent = ref<string>('')

const handleFileChange = (file: UploadUserFile) => {
  docxFile.value = file
}

const handleFileRemove = () => {
  docxFile.value = null
}

const handleConverted = (html: string) => {
  htmlContent.value = html
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
