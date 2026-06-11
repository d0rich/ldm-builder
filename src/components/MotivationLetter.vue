<script setup lang="ts">
import { computedAsync } from '@vueuse/core'
import { remark } from 'remark'
import remarkHtml from 'remark-html'
import templateMd from '../assets/template.md?raw'
import templateJuniorMd from '../assets/template_junior.md?raw'

export interface Replacements {
  poste: string
  entreprise: string
}

const props = withDefaults(defineProps<{
  junior?: boolean
  replacements: Replacements
}>(), {
  junior: false
})

const html = computedAsync(async () => {
  const source = (props.junior ? templateJuniorMd : templateMd)
    .replaceAll('{{POSTE}}', props.replacements.poste)
    .replaceAll('{{ENTREPRISE}}', props.replacements.entreprise)
  const result = await remark().use(remarkHtml).process(source)
  return result.toString()
}, '')
</script>

<template>
  <article class="prose max-w-none" v-html="html" />
</template>
