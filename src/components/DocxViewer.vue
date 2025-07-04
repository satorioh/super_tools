<template>
  <el-button type="primary" text v-if="file" @click="openDocxInNewTab">预览</el-button>
  <!--  <div ref="containerRef" class="docx-container"></div>-->
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { renderAsync } from 'docx-preview'

defineOptions({
  name: 'DocxViewer',
})

const props = defineProps({
  file: {
    type: File,
  },
})

const containerRef = ref<HTMLDivElement | null>(null)

const renderDocx = async (file: File) => {
  if (!containerRef.value) return

  // 清空容器
  containerRef.value.innerHTML = ''

  try {
    // 使用 docx-preview 渲染 DOCX 文件
    await renderAsync(file, containerRef.value)
  } catch (error) {
    console.error('Error rendering DOCX file:', error)
    containerRef.value.innerHTML = '<p>Error rendering document.</p>'
  }
}

const openDocxInNewTab = async () => {
  if (!props.file) {
    console.warn('No file provided to render.')
    return
  }
  const docWindow = window.open('', '_blank')
  const container = document.createElement('div')

  renderAsync(props.file, container)
    .then(() => {
      if (docWindow) {
        // 将容器div添加到新窗口的body中
        docWindow.document.body.appendChild(container)
        docWindow.document.title = '文档预览'
      }
    })
    .catch((err) => {
      console.error('渲染docx失败:', err)
    })
}
</script>

<style lang="scss" scoped>
.docx-container {
  width: 100%;
  height: 100%;
  overflow: auto;
  padding: 20px;
  box-sizing: border-box;

  // docx-preview 的样式
  .docx-preview {
    font-family: Arial, sans-serif;
    line-height: 1.6;
    color: #333;
  }
}
</style>
