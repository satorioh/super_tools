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
  plugins: 'code autoresize autosave link image preview',
  menubar: false,
  branding: false,
  toolbar:
    'undo redo | fontsizeselect formatselect | bold italic forecolor | alignleft aligncenter alignright alignjustify | bullist numlist outdent indent blockquote | link image media | preview toggleMode',

  setup: function (editor) {
    let isSourceMode = false
    let originalContent = ''

    editor.ui.registry.addButton('toggleMode', {
      text: '切换模式',
      onAction: function () {
        if (!isSourceMode) {
          // 进入源码模式，保存原始 HTML 内容
          originalContent = editor.getContent()
          const encoded =
            tinymce.util.Tools.resolve('tinymce.html.Entities').encodeAllRaw(originalContent)
          editor.setContent(
            `<pre id="tinymce-source-mode" style="white-space:pre-wrap;">${encoded}</pre>`,
          )
          isSourceMode = true
        } else {
          // 返回 WYSIWYG 模式
          const pre = editor.getDoc().getElementById('tinymce-source-mode')
          const rawHtml = pre ? pre.innerText : ''
          const decoded = tinymce.util.Tools.resolve('tinymce.html.Entities').decode(rawHtml)
          editor.setContent(decoded)
          isSourceMode = false
        }
      },
    })
  },
}
</script>

<style scoped></style>
