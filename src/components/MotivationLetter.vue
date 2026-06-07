<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { remark } from 'remark'
import remarkHtml from 'remark-html'
import templateMd from '../assets/template.md?raw'

const html = ref('')

onMounted(async () => {
  const result = await remark().use(remarkHtml).process(templateMd)
  html.value = result.toString()
})
</script>

<template>
  <article class="prose max-w-none" v-html="html" />
</template>
