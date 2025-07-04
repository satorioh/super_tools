<template>
  <el-upload
    ref="uploadRef"
    v-model:file-list="fileList"
    class="upload-demo"
    action=""
    :auto-upload="false"
    accept=".docx"
    @change="handleChange"
  >
    <template #trigger>
      <el-button type="primary">上传.docx文件</el-button>
    </template>
  </el-upload>
</template>

<script lang="ts" setup>
import { ref } from 'vue'
import type { UploadInstance, UploadUserFile } from 'element-plus'

defineOptions({
  name: 'DocxUploader',
})

const emit = defineEmits<{
  (e: 'change', file: UploadUserFile): void
}>()

const uploadRef = ref<UploadInstance>()
const fileList = ref<UploadUserFile[]>([])

const handleChange = (file: UploadUserFile) => {
  console.log('File changed:', file)
  emit('change', file)
}
</script>
