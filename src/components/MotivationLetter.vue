<script setup lang="ts">
import { computedAsync } from '@vueuse/core'
import { remark } from 'remark'
import remarkHtml from 'remark-html'
import templateMd from '../assets/template.md?raw'

export interface Replacements {
  poste: string
  entreprise: string
}

const props = defineProps<{
  replacements: Replacements
}>()

const html = computedAsync(async () => {
  const source = templateMd
    .replaceAll('{{POSTE}}', props.replacements.poste)
    .replaceAll('{{ENTREPRISE}}', props.replacements.entreprise)
  const result = await remark().use(remarkHtml).process(source)
  return result.toString()
}, '')
</script>

<template>
  <article class="prose max-w-none" v-html="html" />
</template>
