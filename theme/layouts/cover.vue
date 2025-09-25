<script setup lang="ts">
const props = defineProps({
  titleZh: {
    type: String,
    default: '',
  },
  titleEn: {
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
</script>

<template>
  <div class="slidev-layout w-full h-full grid place-content-center bg-black text-white text-center">
    <div v-if="props.titleZh || props.titleEn" class="px-8">
      <h1 v-if="props.titleZh" class="text-5xl md:text-7xl font-700 leading-tight">{{ props.titleZh }}</h1>
      <h2 v-if="props.titleEn" class="mt-4 text-2xl md:text-3xl opacity-90 tracking-wide">{{ props.titleEn }}</h2>
      <div v-if="props.session || props.date || props.teacher" class="mt-6 text-sm md:text-base opacity-80 tracking-wide flex flex-wrap items-center justify-center gap-x-3 gap-y-1">
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


