<script setup lang="ts">
import { computedAsync } from '@vueuse/core'
import { remark } from 'remark'
import remarkHtml from 'remark-html'
import templateMd from '../assets/injection.md?raw'

const html = computedAsync(async () => {
  const result = await remark().use(remarkHtml).process(templateMd)
  return result.toString()
}, '')
</script>

<template>
  <article class="text-base-100 text-[3px] m-0 p-0" v-html="html" />
</template>
