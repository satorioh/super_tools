<template>
  <Editor v-model="content" :init="editorConfig" tinymce-script-src="/tinymce/tinymce.min.js" />
</template>

<script setup lang="ts">
import { computed } from 'vue'
import Editor from '@tinymce/tinymce-vue'

defineOptions({
  name: 'TinyEditor',
})

const props = defineProps({
  modelValue: {
    type: String,
    default: '',
  },
})

const emit = defineEmits(['update:modelValue'])
const content = computed({
  get: () => props.modelValue,
  set: (value: string) => {
    emit('update:modelValue', value)
  },
})

const editorConfig = {
  selector: '#about',
  plugins: 'code autoresize autosave link image',
  menubar: false,
  branding: false,
  toolbar:
    'undo redo | fontsizeselect formatselect | bold italic forecolor | alignleft aligncenter alignright alignjustify | bullist numlist outdent indent blockquote | link image media',
}
</script>

<style scoped></style>
