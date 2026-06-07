<script setup lang="ts">
import type { Replacements } from './MotivationLetter.vue'

const model = defineModel<Replacements>({ required: true })

const print = () => window.print()
</script>

<template>
  <form class="card bg-base-200 shadow-sm print:hidden" @submit.prevent="print">
    <div class="card-body gap-4">
      <h2 class="card-title">Données de candidature</h2>

      <fieldset class="fieldset">
        <legend class="fieldset-legend">Poste visé</legend>
        <input
          v-model="model.poste"
          type="text"
          placeholder="Développeur Full-Stack"
          class="input w-full"
        />
      </fieldset>

      <fieldset class="fieldset">
        <legend class="fieldset-legend">Entreprise</legend>
        <input
          v-model="model.entreprise"
          type="text"
          placeholder="Acme Corp"
          class="input w-full"
        />
      </fieldset>

      <div class="card-actions justify-end">
        <button type="submit" class="btn btn-primary">
          Imprimer / PDF
        </button>
      </div>
    </div>
  </form>
</template>
