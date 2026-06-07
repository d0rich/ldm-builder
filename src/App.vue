<script setup lang="ts">
import { ref } from 'vue'
import MotivationLetter, { type Replacements } from './components/MotivationLetter.vue'

const replacements = ref<Replacements>({
  poste: 'Développeur Web',
  entreprise: 'Tech Solutions'
})
</script>

<template>
  <main class="max-w-3xl mx-auto px-6 py-12">
    <MotivationLetter :replacements="replacements" />
  </main>
</template>