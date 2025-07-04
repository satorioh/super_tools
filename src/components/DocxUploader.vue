<template>
  <el-upload
    ref="uploadRef"
    v-model:file-list="fileList"
    class="my-uploader"
    action=""
    :auto-upload="false"
    accept=".docx"
    :limit="1"
    :on-exceed="handleExceed"
    :on-remove="handleRemove"
    @change="handleChange"
  >
    <template #trigger>
      <el-button type="primary">上传.docx文件</el-button>
    </template>
  </el-upload>
</template>

<script lang="ts" setup>
import { ref } from 'vue'
import { genFileId } from 'element-plus'
import type { UploadInstance, UploadUserFile, UploadProps, UploadRawFile } from 'element-plus'

defineOptions({
  name: 'DocxUploader',
})

const emit = defineEmits<{
  (e: 'change', file: UploadUserFile): void
  (e: 'remove'): void
}>()

const uploadRef = ref<UploadInstance>()
const fileList = ref<UploadUserFile[]>([])

const handleChange = (file: UploadUserFile) => {
  console.log('File changed:', file)
  emit('change', file)
}

const handleExceed: UploadProps['onExceed'] = (files) => {
  uploadRef.value!.clearFiles()
  const file = files[0] as UploadRawFile
  file.uid = genFileId()
  uploadRef.value!.handleStart(file)
}

const handleRemove: UploadProps['onRemove'] = () => {
  fileList.value = []
  emit('remove')
}
</script>

<style lang="scss" scoped>
.my-uploader {
  display: grid;
  grid-template-columns: 140px 200px;
}
</style>
