<script setup lang="ts">
import { useLocalStorage } from '@vueuse/core'
import MotivationLetter, { type Replacements } from './components/MotivationLetter.vue'
import ReplacementsForm from './components/ReplacementsForm.vue'

const replacements = useLocalStorage<Replacements>('ldm-replacements', {
  poste: 'Développeur Web',
  entreprise: 'Tech Solutions'
})
</script>

<template>
  <main class="max-w-3xl mx-auto px-6 py-12 flex flex-col gap-8">
    <ReplacementsForm v-model="replacements" />
    <MotivationLetter :replacements="replacements" />
  </main>
</template>