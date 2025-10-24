<script setup lang="ts">
import { computed, defineAsyncComponent, onMounted, ref, watch } from 'vue'

type Props = {
  /**
   * Markdown 文件路径，建议以项目根目录为基准，例如："/files/9.27.md"
   * 也可传入相对根目录的路径，如："files/9.27.md"
   */
  src: string
  /**
   * 容器最大高度，支持任意 CSS 长度单位，默认 60vh
   */
  maxHeight?: string
}

const props = defineProps<Props>()

const normalizedSrc = computed(() => {
  if (!props.src)
    return ''
  // 统一转为以根目录开头，便于 import.meta.glob 匹配
  return props.src.startsWith('/') ? props.src : `/${props.src.replace(/^\.\//, '')}`
})

const modules = {
  // 支持从项目根目录匹配任意 md（Slidev + Vite 环境）
  ...(import.meta as any).glob('/**/*.md'),
}

const AsyncContent = ref<ReturnType<typeof defineAsyncComponent> | null>(null)

function resolveModule(path: string) {
  const mod = modules[path]
  if (!mod)
    return null
  return defineAsyncComponent(async () => {
    // 动态导入为一个可渲染的 Vue 组件
    const m = await mod()
    return (m as any).default || m
  })
}

function updateContent() {
  const path = normalizedSrc.value
  AsyncContent.value = path ? resolveModule(path) : null
}

onMounted(updateContent)
watch(() => normalizedSrc.value, updateContent)

const containerStyle = computed(() => ({
  maxHeight: props.maxHeight || '60vh',
}))
</script>

<template>
  <div
    class="overflow-auto rounded-lg border border-neutral-200 dark:border-neutral-700 bg-white/70 dark:bg-black/30 backdrop-blur-sm p-4"
    :style="containerStyle"
  >
    <component v-if="AsyncContent" :is="AsyncContent" />
    <div v-else class="text-sm opacity-70">
      无法加载内容：请检查路径是否正确（示例：/files/xxx.md）
    </div>
  </div>
  
</template>



