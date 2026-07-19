<script setup>
import { inject, computed } from 'vue'
import { FolderKanban, Plus } from 'lucide-vue-next'

const locale = inject('locale')

const translations = {
  en: {
    title: "Projects",
    comingSoon: "Coming Soon",
    description: "Exciting projects are currently in development. Check back soon to explore my latest work — from full-stack applications to open-source contributions.",
    cta: "Stay Tuned"
  },
  de: {
    title: "Projekte",
    comingSoon: "Demnächst verfügbar",
    description: "Spannende Projekte sind derzeit in der Entwicklung. Schauen Sie bald wieder vorbei, um meine neuesten Arbeiten zu entdecken — von Full-Stack-Anwendungen bis hin zu Open-Source-Beiträgen.",
    cta: "Bleiben Sie dran"
  }
}

const t = computed(() => translations[locale.value] || translations.en)
</script>

<template>
  <section class="max-w-4xl mx-auto pb-12">
    <h2 class="text-4xl font-bold text-white mb-12 flex items-center gap-4">
      <FolderKanban class="text-blue-500" /> {{ t.title }}
    </h2>

    <!-- Coming Soon Placeholder -->
    <div class="flex flex-col items-center justify-center text-center py-20 px-8 rounded-3xl border border-dashed border-white/10 bg-white/[0.02] hover:border-blue-500/30 transition-all duration-500">
      <!-- Animated Icon -->
      <div class="w-20 h-20 rounded-full bg-blue-500/10 border border-blue-500/20 flex items-center justify-center mb-8 animate-pulse">
        <Plus class="w-8 h-8 text-blue-400" />
      </div>

      <span class="inline-block px-4 py-1.5 rounded-full bg-blue-500/10 border border-blue-500/20 text-blue-400 text-xs font-bold uppercase tracking-widest mb-6">
        {{ t.comingSoon }}
      </span>

      <p class="text-lg text-slate-400 max-w-lg leading-relaxed mb-8">
        {{ t.description }}
      </p>

      <div class="flex gap-3">
        <a 
          href="https://github.com/brundabharadwaj" 
          target="_blank"
          class="px-6 py-2.5 bg-white/5 border border-white/10 text-white rounded-full text-sm font-bold hover:bg-blue-600 hover:border-blue-500 transition-all duration-300"
        >
          {{ t.cta }}
        </a>
      </div>
    </div>
  </section>
</template>
