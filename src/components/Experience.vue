<script setup>
// 1. MUST import the icons used in the template
import { Briefcase, ChevronRight } from 'lucide-vue-next'

const experience = [

  {
    company: "JP Morgan Chase & Co.",
    role: "SDE 2",
    period: "Jul 2025 - Present",
    points: [
      "Involved in architectural design for Bulk Proxy Management system for India UPI, enabling large-scale data ingestion through optimized Excel file processing.",
      "Led the design and implementation of a high-concurrency batch-processing engine to ensure fault-tolerant proxy uploads.",
      "Optimized microservices architecture to handle high-volume UPI transactions with sub-second latency.",
      "Collaborated on end-to-end design patterns to improve system resilience and data validation for proxy operations."
    ]
  },
 {
    company: "Mercedes Benz R&D",
    role: "Senior Consultant",
    period: "2023 - 2025",
    points: [
      "Engineered a Kotlin migration library to bridge legacy systems with modern Spring Boot microservices.",
      "Architected a cross-functional MB.OS file-management component in Vue.js, reducing company-wide code redundancy.",
      "Automated UI/UX design evaluations via an intelligent review system, cutting processing time by 30%.",
      "Integrated real-time file scanning and security protocols into core storage microservices.",
      "Mentored junior engineers to accelerate onboarding and promote best practices in clean code."
    ]
  },
  {
    company: "Mercedes Benz R&D",
    role: "Consultant",
    period: "2021 - 2023",
    points: ["Automated workflows using RPA", "Integrated BlackDuck security scanning"]
  }
]
</script>

<template>
  <section class="max-w-4xl mx-auto">
    <h2 class="text-4xl font-bold text-white mb-12 flex items-center gap-4">
      <Briefcase class="text-blue-500" /> Career Path
    </h2>
    <div class="space-y-6">
      <div 
        v-for="(job, index) in experience" 
        :key="index" 
        class="group p-8 rounded-3xl border border-white/5 bg-white/[0.02] hover:bg-white/[0.04] transition-all duration-500 hover:border-blue-500/30"
      >
        <div class="flex flex-col md:flex-row justify-between mb-6">
          <div>
            <h3 class="text-2xl font-bold text-white group-hover:text-blue-400 transition">{{ job.role }}</h3>
            <p class="text-lg font-medium text-slate-400">{{ job.company }}</p>
          </div>
          <span class="text-blue-500/50 font-mono font-bold">{{ job.period }}</span>
        </div>
        <ul class="grid grid-cols-1 md:grid-cols-2 gap-4">
          <li v-for="point in job.points" :key="point" class="flex gap-3 text-sm text-slate-400">
            <ChevronRight class="w-4 h-4 text-blue-500 shrink-0" /> {{ point }}
          </li>
        </ul>
      </div>
    </div>
  </section>
</template>