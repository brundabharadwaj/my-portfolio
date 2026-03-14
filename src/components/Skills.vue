<script setup>
import { Code2 } from 'lucide-vue-next'

const skillGroups = [
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
]
</script>

<template>
  <section class="max-w-4xl mx-auto">
    <h2 class="text-4xl font-bold text-white mb-12 flex items-center gap-4">
      <Code2 class="text-blue-500" /> Technical Stack
    </h2>
    <div 
  v-for="skill in skillGroups" 
  :key="skill.title"
  :class="[
    // Base classes applied to ALL cards
    'p-8 rounded-3xl border transition-all duration-500 cursor-default',
    
    // Hover effect applied to ALL cards
    'hover:border-blue-500/60 hover:shadow-lg hover:shadow-blue-500/5',
    
    // Conditional classes
    skill.highlight 
      ? 'bg-gradient-to-br from-blue-600/20 to-transparent border-blue-500/20' 
      : 'bg-white/[0.03] border-white/10'
  ]"
>
  <h3 class="text-xl font-bold text-white mb-4">{{ skill.title }}</h3>
  <p class="text-slate-400">{{ skill.description }}</p>
    </div>
  </section>
</template>
<style>
@import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap');

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