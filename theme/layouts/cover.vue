<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps({
  titleZh: {
    type: String,
    default: '',
  },
  session: {
    // 第几次课，例如：第 3 次课 / Lesson 3
    type: String,
    default: '',
  },
  date: {
    // 上课日期，例如：2025-09-23
    type: String,
    default: '',
  },
  teacher: {
    // 授课老师，例如：张三
    type: String,
    default: '',
  },
})

// 根据标题长度计算CSS类
const titleClass = computed(() => {
  if (!props.titleZh) return 'cover-title'
  
  const length = props.titleZh.length
  if (length <= 4) return 'cover-title short-title'
  if (length <= 8) return 'cover-title medium-title'
  if (length <= 12) return 'cover-title long-title'
  return 'cover-title extra-long-title'
})
</script>

<template>
  <div class="slidev-layout cover-layout w-full h-full grid place-content-center bg-white text-black text-center">
    <div v-if="props.titleZh" class="px-8">
      <h1 v-if="props.titleZh" :class="titleClass">{{ props.titleZh }}</h1>
      <div v-if="props.session || props.date || props.teacher" class="cover-subtitle flex flex-wrap items-center justify-center gap-x-3 gap-y-1">
        <span v-if="props.session">{{ props.session }}</span>
        <span v-if="props.date" class="opacity-70">•</span>
        <span v-if="props.date">{{ props.date }}</span>
        <span v-if="props.teacher" class="opacity-70">•</span>
        <span v-if="props.teacher">{{ props.teacher }}</span>
      </div>
    </div>
    <div v-else class="px-8">
      <slot />
    </div>
  </div>
  
</template>


