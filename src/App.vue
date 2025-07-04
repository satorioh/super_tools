<template>
  <el-config-provider :z-index="zIndex">
    <RouterView />
  </el-config-provider>
</template>

<script setup lang="ts">
import { RouterView } from 'vue-router'
import { ElConfigProvider } from 'element-plus'

const zIndex = 3000
</script>

<style scoped></style>
