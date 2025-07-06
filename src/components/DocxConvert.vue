<template>
  <div id="docx-content" class="docx-content"></div>
</template>

<script setup lang="ts">
import { defineOptions, defineProps, watch } from 'vue'
import mammoth from 'mammoth'

defineOptions({
  name: 'DocxConvert',
})

const props = defineProps({
  file: {
    type: File,
  },
})

const emit = defineEmits<{
  (e: 'converted', html: string): void
}>()

const convert = async (file: File) => {
  if (!file) {
    console.warn('No file provided for conversion.')
    return
  }

  mammoth
    .convertToHtml({ arrayBuffer: file })
    .then((result) => {
      const html = result.value // The generated HTML
      const messages = result.messages // Any messages, e.g. warnings
      console.log('Converted HTML:', html)
      console.log('Messages:', messages)
      emit('converted', html)
    })
    .catch((err) => {
      console.error('Error converting DOCX to HTML:', err)
    })
}

watch(
  () => props.file,
  (newFile) => {
    if (newFile) {
      convert(newFile)
    }
  },
  { immediate: true },
)
</script>

<style scoped></style>
