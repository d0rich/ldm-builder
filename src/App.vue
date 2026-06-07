<script setup lang="ts">
import { computed } from 'vue'
import { useLocalStorage } from '@vueuse/core'
import { useHead } from '@unhead/vue'
import MotivationLetter, { type Replacements } from './components/MotivationLetter.vue'
import ReplacementsForm from './components/ReplacementsForm.vue'

const BASE_URL = 'https://ldm.d0rich.me'
const OG_TITLE = 'LDM Builder'
const DESCRIPTION = '📝 Générez votre LDM personnalisée en PDF en quelques clics.'
const OG_IMAGE = `${BASE_URL}/og/image.jpg`

const replacements = useLocalStorage<Replacements>('ldm-replacements', {
  poste: 'Développeur Web',
  entreprise: 'Tech Solutions'
})

const slugify = (s: string) => s.trim().replace(/\s+/g, '_')

const title = computed(
  () => `LdM__${slugify(replacements.value.poste)}__${slugify(replacements.value.entreprise)}`
)

useHead({
  title,
  htmlAttrs: { lang: 'fr' },
  meta: [
    { name: 'description', content: DESCRIPTION },
    { name: 'author', content: 'Nikolai Dorofeev' },

    // Open Graph
    { property: 'og:type', content: 'website' },
    { property: 'og:url', content: BASE_URL },
    { property: 'og:title', content: OG_TITLE },
    { property: 'og:description', content: DESCRIPTION },
    { property: 'og:image', content: OG_IMAGE },
    { property: 'og:image:alt', content: 'LDM Builder preview' },
    { property: 'og:locale', content: 'fr_FR' },
    { property: 'og:site_name', content: 'LDM Builder' },

    // Twitter Card
    { name: 'twitter:card', content: 'summary_large_image' },
    { name: 'twitter:title', content: OG_TITLE },
    { name: 'twitter:description', content: DESCRIPTION },
    { name: 'twitter:image', content: OG_IMAGE },
  ],
  link: [
    { rel: 'canonical', href: BASE_URL },
  ],
})
</script>

<template>
  <main class="max-w-3xl mx-auto px-6 py-12 flex flex-col gap-8">
    <ReplacementsForm v-model="replacements" />
    <MotivationLetter :replacements="replacements" />
  </main>
</template>