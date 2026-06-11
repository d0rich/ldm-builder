<script setup lang="ts">
import { computed } from 'vue'
import { useLocalStorage } from '@vueuse/core'
import { useHead } from '@unhead/vue'
import MotivationLetter, { type Replacements } from './components/MotivationLetter.vue'
import ReplacementsForm from './components/ReplacementsForm.vue'
import Injection from './components/Injection.vue'

const showInjection = useLocalStorage('ldm-show-injection', false)
const modeJunior = useLocalStorage('ldm-mode-junior', false)

const replacements = useLocalStorage<Replacements>('ldm-replacements', {
  poste: 'Développeur Web',
  entreprise: 'Tech Solutions'
})

const slugify = (s: string) => s.trim().replace(/\s+/g, '_')

const title = computed(
  () => `LdM__${slugify(replacements.value.poste)}__${slugify(replacements.value.entreprise)}`
)

useHead({ title })
</script>

<template>
  <main class="max-w-3xl mx-auto px-6 py-12 flex flex-col gap-8">
    <div>
      <ReplacementsForm 
        v-model="replacements" 
        v-model:showInjection="showInjection" 
        v-model:modeJunior="modeJunior" 
      />
      <Injection v-if="showInjection" />
    </div>
    <MotivationLetter :replacements="replacements" :junior="modeJunior" />
  </main>
</template>