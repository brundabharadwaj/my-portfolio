<script setup>
import { ref, inject, computed } from 'vue'
import { Code2, GraduationCap, ChevronLeft, ChevronRight, ExternalLink } from 'lucide-vue-next'

const locale = inject('locale')
const activeIndex = ref(0)

const translations = {
  en: {
    title: "Technical Stack",
    certTitle: "Certifications",
    viewFull: "View Full Image",
    viewCert: "View Certificate",
    dateLabel: "Issued",
    skills: [
      {
        title: "Backend Architecture",
        description: "Java, Spring Boot, Kotlin, Microservices, OracleDB, PostgreSQL",
        highlight: true
      },
      {
        title: "Frontend",
        description: "Vue.js, React, TypeScript, Tailwind CSS",
        highlight: false
      },
      {
        title: "Cloud & DevOps",
        description: "Azure, Docker, Kubernetes, CI/CD",
        highlight: false
      },
      {
        title: "Automation",
        description: "RPA, Kafka, DataDog, BlackDuck",
        highlight: false
      }
    ],
    certs: [
      {
        title: "Build with AI Bootcamp",
        issuer: "Google for Developers",
        date: "July 15, 2026",
        image: "certificates/build_with_ai.png",
        description: "Demonstrated the technical skills required to build AI agents, architect workflows, and integrate generative AI into production-ready systems."
      },
      {
        title: "AI Fluency: Framework & Foundations",
        issuer: "Anthropic",
        date: "July 2026",
        image: "certificates/ai_fluency.jpg",
        description: "Completed foundational training on framework architectures, prompt construction, and model characteristics for Anthropic Claude models."
      },
      {
        title: "Claude Code 101",
        issuer: "Anthropic",
        date: "July 2026",
        image: "certificates/claude_code_101.jpg",
        description: "Completed advanced coursework on AI-driven terminal editing, terminal tool execution, and code maintenance using Claude Code."
      }
    ]
  },
  de: {
    title: "Technologie-Stack",
    certTitle: "Zertifikate",
    viewFull: "Vollbild anzeigen",
    viewCert: "Zertifikat ansehen",
    dateLabel: "Ausgestellt",
    skills: [
      {
        title: "Backend-Architektur",
        description: "Java, Spring Boot, Kotlin, Microservices, OracleDB, PostgreSQL",
        highlight: true
      },
      {
        title: "Frontend",
        description: "Vue.js, React, TypeScript, Tailwind CSS",
        highlight: false
      },
      {
        title: "Cloud & DevOps",
        description: "Azure, Docker, Kubernetes, CI/CD",
        highlight: false
      },
      {
        title: "Automatisierung",
        description: "RPA, Kafka, DataDog, BlackDuck",
        highlight: false
      }
    ],
    certs: [
      {
        title: "Build with AI Bootcamp",
        issuer: "Google for Developers",
        date: "15. Juli 2026",
        image: "certificates/build_with_ai.png",
        description: "Nachweis der erforderlichen technischen Fähigkeiten zum Erstellen von KI-Agenten, zur Entwicklung von Workflows und zur Integration generativer KI in produktionsreife Systeme."
      },
      {
        title: "AI Fluency: Framework & Foundations",
        issuer: "Anthropic",
        date: "Juli 2026",
        image: "certificates/ai_fluency.jpg",
        description: "Abschluss der Grundlagenschulung zu Framework-Architekturen, Prompt-Konstruktion und Modelleigenschaften für Anthropic Claude-Modelle."
      },
      {
        title: "Claude Code 101",
        issuer: "Anthropic",
        date: "Juli 2026",
        image: "certificates/claude_code_101.jpg",
        description: "Abschluss des Fortgeschrittenenkurses über KI-gestützte Terminalbearbeitung, Terminal-Tool-Ausführung und Codewartung mit Claude Code."
      }
    ]
  }
}

const t = computed(() => translations[locale.value] || translations.en)

const nextSlide = () => {
  activeIndex.value = (activeIndex.value + 1) % t.value.certs.length
}
const prevSlide = () => {
  const len = t.value.certs.length
  activeIndex.value = (activeIndex.value - 1 + len) % len
}
</script>

<template>
  <section class="max-w-4xl mx-auto pb-12">
    <!-- Technical Stack Section -->
    <h2 class="text-4xl font-bold text-white mb-12 flex items-center gap-4">
      <Code2 class="text-blue-500" /> {{ t.title }}
    </h2>
    <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-16">
      <div 
        v-for="skill in t.skills" 
        :key="skill.title"
        :class="[
          'p-8 rounded-3xl border transition-all duration-500 cursor-default',
          'hover:border-blue-500/60 hover:shadow-lg hover:shadow-blue-500/5',
          skill.highlight 
            ? 'bg-gradient-to-br from-blue-600/20 to-transparent border-blue-500/20' 
            : 'bg-white/[0.03] border-white/10'
        ]"
      >
        <h3 class="text-xl font-bold text-white mb-4">{{ skill.title }}</h3>
        <p class="text-slate-400">{{ skill.description }}</p>
      </div>
    </div>

    <!-- Certifications Section -->
    <div class="mt-20">
      <h2 class="text-4xl font-bold text-white mb-12 flex items-center gap-4">
        <GraduationCap class="text-blue-500" /> {{ t.certTitle }}
      </h2>
      
      <!-- Slider Carousel Container -->
      <div class="relative max-w-2xl mx-auto group/slider">
        <!-- Main Slider Card -->
        <div class="overflow-hidden rounded-3xl border border-white/10 bg-white/[0.02] backdrop-blur-xl shadow-2xl p-6 transition-all duration-500 hover:border-blue-500/30">
          <div class="flex flex-col md:flex-row gap-8 items-center">
            <!-- Image Area -->
            <div class="w-full md:w-1/2 overflow-hidden rounded-2xl border border-white/10 bg-black/40 aspect-[4/3] flex items-center justify-center relative group">
              <img 
                :src="t.certs[activeIndex].image" 
                :alt="t.certs[activeIndex].title"
                class="w-full h-full object-cover transition-transform duration-500 group-hover:scale-105"
              />
              <a 
                :href="t.certs[activeIndex].image" 
                target="_blank" 
                class="absolute inset-0 bg-black/60 opacity-0 group-hover:opacity-100 transition-opacity duration-300 flex items-center justify-center text-white font-semibold gap-2 text-sm cursor-pointer"
              >
                <ExternalLink class="w-4 h-4" /> {{ t.viewFull }}
              </a>
            </div>
            
            <!-- Details Area -->
            <div class="w-full md:w-1/2 text-left flex flex-col justify-between h-full min-h-[160px]">
              <div>
                <span class="inline-block px-3 py-1 rounded-full bg-blue-500/10 border border-blue-500/20 text-blue-400 text-xs font-bold tracking-wider mb-4 uppercase">
                  {{ t.certs[activeIndex].issuer }}
                </span>
                <h3 class="text-2xl font-bold text-white mb-3 tracking-tight">
                  {{ t.certs[activeIndex].title }}
                </h3>
                <p class="text-sm text-slate-400 leading-relaxed mb-4">
                  {{ t.certs[activeIndex].description }}
                </p>
              </div>
              <div class="flex items-center justify-between mt-auto pt-4 border-t border-white/5">
                <span class="text-xs text-slate-500 font-mono">{{ t.dateLabel }}: {{ t.certs[activeIndex].date }}</span>
                <a 
                  :href="t.certs[activeIndex].image" 
                  target="_blank" 
                  class="text-xs text-blue-400 hover:text-blue-300 flex items-center gap-1 font-bold tracking-wider uppercase transition-colors cursor-pointer"
                >
                  {{ t.viewCert }} <ExternalLink class="w-3 h-3" />
                </a>
              </div>
            </div>
          </div>
        </div>

        <!-- Navigation Buttons -->
        <!-- Left Arrow -->
        <button 
          @click="prevSlide" 
          class="absolute top-1/2 -left-4 md:-left-12 -translate-y-1/2 w-10 h-10 rounded-full border border-white/10 bg-[#050505]/80 hover:bg-blue-600 hover:border-blue-500 text-white flex items-center justify-center transition-all duration-300 opacity-0 group-hover/slider:opacity-100 focus:opacity-100 shadow-lg cursor-pointer"
          aria-label="Previous slide"
        >
          <ChevronLeft class="w-5 h-5" />
        </button>
        <!-- Right Arrow -->
        <button 
          @click="nextSlide" 
          class="absolute top-1/2 -right-4 md:-right-12 -translate-y-1/2 w-10 h-10 rounded-full border border-white/10 bg-[#050505]/80 hover:bg-blue-600 hover:border-blue-500 text-white flex items-center justify-center transition-all duration-300 opacity-0 group-hover/slider:opacity-100 focus:opacity-100 shadow-lg cursor-pointer"
          aria-label="Next slide"
        >
          <ChevronRight class="w-5 h-5" />
        </button>

        <!-- Pagination Dots -->
        <div class="flex justify-center gap-2 mt-6">
          <button 
            v-for="(cert, idx) in t.certs" 
            :key="idx"
            @click="activeIndex = idx"
            class="w-2.5 h-2.5 rounded-full transition-all duration-300 cursor-pointer"
            :class="activeIndex === idx ? 'bg-blue-500 w-6' : 'bg-white/20 hover:bg-white/40'"
            :aria-label="'Go to slide ' + (idx + 1)"
          ></button>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
/* Scoped transition optimizations if needed */
</style>