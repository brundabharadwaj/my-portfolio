<script setup>
import { ref, onMounted, provide, computed } from 'vue'
import { Github, Linkedin, Mail, ExternalLink, MapPin, Code2, Briefcase, GraduationCap, ChevronRight, Sparkles, Home } from 'lucide-vue-next'
import Skills from './components/Skills.vue'
import Experience from './components/Experience.vue'
import Projects from './components/Projects.vue'
// State for active page/section
const activeSection = ref('home') 

// State for scroll animation (kept for nav styling)
const isScrolled = ref(false)
onMounted(() => {
  window.addEventListener('scroll', () => {
    isScrolled.value = window.scrollY > 20
  })
})

const locale = ref('en')
provide('locale', locale)

const toggleLanguage = () => {
  locale.value = locale.value === 'en' ? 'de' : 'en'
}

const translations = {
  en: {
    nav: {
      experience: "Experience",
      skills: "Skills",
      projects: "Projects"
    },
    home: {
      badge: "Available for Innovation",
      cta: "View My Work"
    },
    footer: "Brunda M Bharadwaj © 2026 • Built with Vue 3"
  },
  de: {
    nav: {
      experience: "Erfahrung",
      skills: "Fähigkeiten",
      projects: "Projekte"
    },
    home: {
      badge: "Verfügbar für Innovationen",
      cta: "Meine Arbeit ansehen"
    },
    footer: "Brunda M Bharadwaj © 2026 • Erstellt mit Vue 3"
  }
}

const t = computed(() => translations[locale.value])
</script>

<template>
  <div class="bg-[#050505] text-slate-300 min-h-screen font-sans selection:bg-blue-500/30 overflow-x-hidden">
    
    <!-- 1. NAVIGATION (Updated with Click Events and Language Toggle) -->
    <nav :class="['fixed top-6 left-1/2 -translate-x-1/2 z-50 transition-all duration-500 px-6 py-3 rounded-full border border-white/10 flex gap-8 items-center backdrop-blur-xl', 
      isScrolled ? 'w-[90%] max-w-2xl bg-white/5 shadow-2xl' : 'w-full max-w-4xl bg-transparent']">
      
      <!-- Clicking logo returns to Home -->
      <button @click="activeSection = 'home'" class="text-white font-black tracking-tighter text-xl cursor-pointer">
        BMB<span class="text-blue-500">.</span>
      </button>

      <div class="hidden md:flex gap-6 text-sm font-medium uppercase tracking-widest">
        <button 
          @click="activeSection = 'work'" 
          :class="['transition cursor-pointer', activeSection === 'work' ? 'text-blue-400' : 'hover:text-white']">
          {{ t.nav.experience }}
        </button>
        <button 
          @click="activeSection = 'skills'" 
          :class="['transition cursor-pointer', activeSection === 'skills' ? 'text-blue-400' : 'hover:text-white']">
          {{ t.nav.skills }}
        </button>
        <button 
          @click="activeSection = 'projects'" 
          :class="['transition cursor-pointer', activeSection === 'projects' ? 'text-blue-400' : 'hover:text-white']">
          {{ t.nav.projects }}
        </button>
      </div>

      <div class="ml-auto flex gap-4 items-center border-l border-white/10 pl-6">
        <a href="https://github.com/brundabharadwaj" target="_blank" class="hover:scale-110 transition"><Github class="w-5 h-5" /></a>
        <a href="https://www.linkedin.com/in/brunda-m-bharadwaj-629571327/" target="_blank" class="hover:scale-110 transition"><Linkedin class="w-5 h-5 text-blue-400" /></a>
        
        <!-- Language Switcher -->
        <button 
          @click="toggleLanguage" 
          class="relative flex items-center justify-between w-16 h-8 rounded-full p-1 bg-white/5 border border-white/10 cursor-pointer transition-all duration-300 hover:border-blue-500/50 focus:outline-none"
          aria-label="Toggle language"
        >
          <!-- Sliding indicator -->
          <div 
            class="absolute top-1 bottom-1 w-7 rounded-full bg-blue-600/80 shadow-md shadow-blue-500/20 transition-all duration-300"
            :class="locale === 'en' ? 'left-1' : 'left-8'"
          ></div>
          <!-- EN Label -->
          <span 
            class="z-10 text-[10px] font-extrabold tracking-wider w-6 text-center transition-colors duration-300"
            :class="locale === 'en' ? 'text-white' : 'text-slate-500 hover:text-slate-400'"
          >EN</span>
          <!-- DE Label -->
          <span 
            class="z-10 text-[10px] font-extrabold tracking-wider w-6 text-center transition-colors duration-300"
            :class="locale === 'de' ? 'text-white' : 'text-slate-500 hover:text-slate-400'"
          >DE</span>
        </button>
      </div>
    </nav>

    <!-- MAIN CONTENT AREA -->
    <main class="relative pt-32 pb-20 px-6">
      <!-- Background Glow -->
      <div class="absolute top-0 left-1/2 -translate-x-1/2 w-full max-w-4xl h-[500px] bg-blue-600/10 blur-[120px] rounded-full -z-10"></div>

      <Transition name="fade" mode="out-in">
        <!-- SECTION: HOME -->
        <section v-if="activeSection === 'home'" key="home" class="max-w-4xl mx-auto text-center pt-20">
          <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-blue-500/10 border border-blue-500/20 text-blue-400 text-xs font-bold uppercase tracking-widest mb-8 animate-pulse">
            <Sparkles class="w-3 h-3" /> {{ t.home.badge }}
          </div>
          <h1 class="text-6xl md:text-8xl font-black text-white mb-8 tracking-tighter">
            Brunda M <br/> <span class="bg-gradient-to-r from-blue-400 via-cyan-400 to-indigo-500 bg-clip-text text-transparent">Bharadwaj</span>
          </h1>
          <p class="text-xl md:text-2xl text-slate-400 max-w-2xl mx-auto leading-relaxed">
            <span v-if="locale === 'en'">
              SDE 2 at <span class="text-white">JP Morgan Chase</span>. 
              Crafting high-performance backend systems and elegant frontend interfaces.
            </span>
            <span v-else>
              Software-Entwickler 2 bei <span class="text-white">JP Morgan Chase</span>. 
              Entwicklung von Hochleistungs-Backendsystemen und eleganten Frontend-Benutzeroberflächen.
            </span>
          </p>
          <div class="mt-12 flex justify-center gap-4">
             <button @click="activeSection = 'work'" class="px-8 py-3 bg-blue-600 text-white rounded-full font-bold hover:bg-blue-500 transition">{{ t.home.cta }}</button>
          </div>
        </section>

        <!-- SECTION: EXPERIENCE -->
         <Experience v-else-if="activeSection === 'work'" key="work" class="max-w-4xl mx-auto"/>
        
        <!-- SECTION: SKILLS -->
        <Skills v-else-if="activeSection === 'skills'" key="skills" />

        <!-- SECTION: PROJECTS -->
        <Projects v-else-if="activeSection === 'projects'" key="projects" />
      </Transition>
    </main>

    <footer class="fixed bottom-0 w-full py-6 text-center bg-[#050505]/80 backdrop-blur-md border-t border-white/5">
      <p class="text-xs text-slate-500">{{ t.footer }}</p>
    </footer>
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap');

body {
  font-family: 'Plus Jakarta Sans', sans-serif;
  margin: 0;
  background: #050505;
}

/* Transition for switching pages */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease, transform 0.3s ease;
}

.fade-enter-from {
  opacity: 0;
  transform: translateY(10px);
}

.fade-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}

/* Custom Scrollbar */
::-webkit-scrollbar { width: 8px; }
::-webkit-scrollbar-track { background: #050505; }
::-webkit-scrollbar-thumb { background: #1e293b; border-radius: 10px; }
::-webkit-scrollbar-thumb:hover { background: #3b82f6; }
</style>