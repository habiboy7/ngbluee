<template>
  <div class="min-h-screen bg-black text-white font-manrope flex flex-col">
    <!-- Top Bar -->
    <header
      class="w-full max-w-7xl mx-auto px-4 sm:px-6 lg:px-12 py-6 md:py-10 flex items-center justify-between z-10"
    >
      <button
        @click="goBack"
        class="group inline-flex items-center gap-2.5 px-5 py-2.5 rounded-full border border-white/10 bg-white/5 text-base font-bold tracking-wider text-white hover:bg-white hover:text-black hover:border-white transition-all duration-300 cursor-pointer shadow-md hover:shadow-lg"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="18"
          height="18"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2.5"
          stroke-linecap="round"
          stroke-linejoin="round"
          class="transform group-hover:-translate-x-1.5 transition-transform"
        >
          <line x1="19" y1="12" x2="5" y2="12"></line>
          <polyline points="12 19 5 12 12 5"></polyline>
        </svg>
        <span>Back</span>
      </button>

      <div class="font-sofia sm:text-xs lg:text-3xl font-bold uppercase tracking-tight">
        Showcase Details
      </div>
    </header>

    <!-- Main Content Container -->
    <main class="flex-grow flex items-center justify-center py-6 sm:py-10">
      <!-- Loading State -->
      <div v-if="loading" class="flex flex-col items-center gap-4 py-20 text-neutral-400">
        <svg class="animate-spin h-8 w-8 text-purple-500" fill="none" viewBox="0 0 24 24">
          <circle
            class="opacity-25"
            cx="12"
            cy="12"
            r="10"
            stroke="currentColor"
            stroke-width="4"
          ></circle>
          <path
            class="opacity-75"
            fill="currentColor"
            d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"
          ></path>
        </svg>
        <span class="text-sm font-bold tracking-widest uppercase">Loading Project...</span>
      </div>

      <!-- Error / Not Found State -->
      <div v-else-if="!project" class="text-center py-20 px-6 max-w-md mx-auto">
        <h2 class="text-2xl font-bold font-sofia mb-4 text-red-500">PROJECT NOT FOUND</h2>
        <p class="text-neutral-400 mb-8 text-sm">
          We couldn't retrieve the project details. It may have been removed or you typed an invalid
          ID.
        </p>
        <button
          @click="goBack"
          class="px-8 py-3 rounded-full bg-white text-black font-bold text-xs uppercase tracking-wider hover:bg-neutral-200 transition-all cursor-pointer"
        >
          Return to Portfolio
        </button>
      </div>

      <!-- Project Detail Layout -->
      <div
        v-else
        class="w-full max-w-7xl mx-auto px-4 sm:px-6 lg:px-12 grid grid-cols-1 lg:grid-cols-12 gap-8 lg:gap-16 items-start"
      >
        <!-- Left Side: Image Showcase -->
        <div class="lg:col-span-7 flex flex-col gap-6 w-full detail-left">
          <!-- Main Screenshot mockup container -->
          <div
            class="relative w-full aspect-[4/3] rounded-3xl overflow-hidden bg-neutral-900 border border-white/10 group shadow-2xl"
          >
            <Transition name="image-fade" mode="out-in">
              <img
                :key="activeImage"
                :src="activeImage"
                :alt="project.title"
                class="w-full h-full object-cover select-none"
              />
            </Transition>

            <!-- Vignette overlay -->
            <div
              class="absolute inset-0 bg-gradient-to-t from-black/40 via-transparent to-black/10 pointer-events-none"
            ></div>

            <!-- Border highlights -->
            <div
              class="absolute inset-0 border border-white/5 pointer-events-none rounded-3xl"
            ></div>
          </div>

          <!-- Feature Description Card -->
          <div
            v-if="activeDesc"
            class="px-6 py-5 rounded-2xl bg-white/5 border border-white/5 backdrop-blur-sm shadow-xl flex flex-col gap-1.5 transition-all duration-300"
          >
            <span
              class="font-sofia text-[10px] lg:text-2xl font-extrabold text-emerald-500 uppercase tracking-normal"
              >{{ activeFeatureTitle }}</span
            >
            <p class="text-sm text-neutral-300 leading-relaxed font-manrope">{{ activeDesc }}</p>
          </div>
        </div>

        <!-- Right Side: Details and Features -->
        <div class="lg:col-span-5 flex flex-col gap-8 w-full detail-right">
          <!-- Headline -->
          <div>
            <h1
              class="font-bold font-sofia text-4xl sm:text-5xl lg:text-6xl text-white uppercase tracking-tighter leading-none"
            >
              {{ project.title }}
            </h1>

            <p v-if="project.tagline" class="font-manrope text-xs lg:text-base mt-3 font-medium text-justify">
              {{ project.tagline }}
            </p>
          </div>

          <!-- Specifications Table -->
          <div class="grid grid-cols-2 gap-4 border-t border-b border-white/10 py-6">
            <div>
              <span
                class="block font-sofia text-[10px] lg:text-2xl font-extrabold text-emerald-500 uppercase tracking-normal mb-1"
                >My Role</span
              >
              <span class="text-sm font-bold text-white uppercase tracking-tight">{{
                project.role || 'Developer'
              }}</span>
            </div>
            <div>
              <span
                class="block font-sofia text-[10px] lg:text-2xl font-extrabold uppercase tracking-normal text-emerald-500 mb-1"
                >Timeline</span
              >
              <span class="text-sm font-bold text-white uppercase tracking-tight">{{
                project.year || '2025'
              }}</span>
            </div>
          </div>

          <!-- Description -->
          <div class="space-y-4">
            <h3
              class="font-sofia text-xs lg:text-2xl font-extrabold uppercase tracking-normal text-emerald-500"
            >
              Project Overview
            </h3>
            <p
              class="text-sm lg:text-base leading-relaxed text-justify whitespace-pre-line font-manrope"
            >
              {{ project.description }}
            </p>
          </div>

          <!-- Interactive Features List -->
          <div v-if="featuresList.length > 0" class="space-y-4">
            <h3
              class="font-sofia text-xs lg:text-2xl font-extrabold uppercase tracking-normal text-emerald-500"
            >
              Core Features
            </h3>
            <div class="space-y-2">
              <div
                v-for="(feat, index) in featuresList"
                :key="index"
                @mouseenter="hoverFeature(feat)"
                @click="selectFeature(feat)"
                class="group flex items-start gap-4 p-4 rounded-2xl border transition-all duration-300 cursor-pointer select-none"
                :class="[
                  activeFeatureTitle === feat
                    ? 'bg-white/10 border-white text-white translate-x-1'
                    : 'bg-white/5 border-white/5 hover:border-white/20 text-neutral-400 hover:text-white',
                ]"
              >
                <span
                  class="text-xs font-bold tracking-wider text-emerald-500 group-hover:text-emerald-300 mt-0.5"
                >
                  0{{ index + 1 }}
                </span>

                <div class="flex-1">
                  <span
                    class="block text-sm font-bold font-manrope transition-transform group-hover:translate-x-0.5 duration-300"
                  >
                    {{ feat }}
                  </span>
                </div>

                <!-- Arrow indicator -->
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="14"
                  height="14"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="3"
                  class="self-center transform transition-all duration-300"
                  :class="
                    activeFeatureTitle === feat
                      ? 'opacity-100 translate-x-0'
                      : 'opacity-0 -translate-x-2'
                  "
                >
                  <line x1="5" y1="12" x2="19" y2="12"></line>
                  <polyline points="12 5 19 12 12 19"></polyline>
                </svg>
              </div>
            </div>
          </div>

          <!-- Technologies Tag List -->
          <div v-if="project.tech && project.tech.length > 0" class="space-y-4 pt-2">
            <h3
              class="font-sofia text-xs lg:text-2xl font-extrabold uppercase tracking-normal text-emerald-500"
            >
              Tech Stack
            </h3>
            <div class="flex flex-wrap gap-2.5">
              <span
                v-for="(techItem, index) in project.tech"
                :key="index"
                class="px-4 py-2 border border-white/10 rounded-full text-xs font-bold text-neutral-300 hover:bg-white hover:text-black hover:border-white transition-all duration-300 cursor-default backdrop-blur-sm"
              >
                {{ techItem }}
              </span>
            </div>
          </div>

          <!-- Links -->
          <div class="flex flex-wrap gap-4 pt-6 border-t border-white/10 mt-2">
            <a
              v-if="project.demo_url"
              :href="project.demo_url"
              target="_blank"
              rel="noopener noreferrer"
              class="font-manrope flex-1 min-w-[140px] inline-flex items-center justify-center gap-2 px-6 py-3.5 rounded-full bg-white text-black font-bold text-xs uppercase tracking-wider hover:bg-neutral-200 transition-all duration-300 shadow-md hover:shadow-lg text-center"
            >
              <span>Live Website</span>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2.5"
                class="w-4 h-4"
              >
                <line x1="7" y1="17" x2="17" y2="7"></line>
                <polyline points="7 7 17 7 17 17"></polyline>
              </svg>
            </a>

            <a
              v-if="project.github_url"
              :href="project.github_url"
              target="_blank"
              rel="noopener noreferrer"
              class="flex-1 min-w-[140px] inline-flex items-center justify-center gap-2 px-6 py-3.5 rounded-full border border-white/20 bg-white/5 text-white font-bold text-xs uppercase tracking-wider hover:bg-white hover:text-black hover:border-white transition-all duration-300 text-center"
            >
              <span>Github Code</span>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2.5"
                class="w-4 h-4"
              >
                <path
                  d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"
                ></path>
              </svg>
            </a>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, nextTick } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import { supabase } from '../lib/supabase'
import gsap from 'gsap'

const route = useRoute()
const router = useRouter()
const loading = ref(true)
const project = ref(null)

const activeImage = ref('')
const activeFeatureTitle = ref('')
const activeDesc = ref('')


const featuresList = computed(() => {
  if (!project.value) return []
  if (project.value.features && Array.isArray(project.value.features)) {
    return project.value.features.filter((f) => f && f.trim() !== '')
  }

  if (project.value.screenshots && Array.isArray(project.value.screenshots)) {
    return project.value.screenshots.map((s) => s.title).filter((t) => t && t.trim() !== '')
  }

  return []
})

// Update left image and descriptor state on hover
const hoverFeature = (featureTitle) => {
  if (!project.value) return
  activeFeatureTitle.value = featureTitle

  // Find corresponding
  if (project.value.screenshots && Array.isArray(project.value.screenshots)) {
    const match = project.value.screenshots.find(
      (s) => s.title && s.title.trim().toLowerCase() === featureTitle.trim().toLowerCase(),
    )
    if (match && match.image_url) {
      activeImage.value = match.image_url
      activeDesc.value = match.desc || ''
      return
    }
  }

  // Fallback to main image
  activeImage.value = project.value.image_url
  activeDesc.value = ''
}

// Handle feature selection
const selectFeature = (featureTitle) => {
  hoverFeature(featureTitle)
}

// Navigates back
const goBack = () => {
  if (window.history.state && window.history.state.back) {
    router.back()
  } else {
    router.push('/')
  }
}

const slugify = (text) => {
  return text
    .toString()
    .toLowerCase()
    .trim()
    .replace(/\s+/g, '-')
    .replace(/[^\w-]+/g, '')
    .replace(/--+/g, '-')
    .replace(/^-+/, '')
    .replace(/-+$/, '')
}

const fetchProjectDetails = async () => {
  const slug = route.params.slug
  loading.value = true

  try {
    // Fetch all projects from Supabase to find a matching slug
    const { data, error } = await supabase.from('projects').select('*')
    if (error) throw error

    if (data) {
      // Try matching by slug, or by ID (in case direct UUID link is accessed)
      const match = data.find((p) => slugify(p.title) === slug || p.id === slug)
      project.value = match || null
    }

    // Initialize display image states
    if (project.value) {
      activeImage.value = project.value.image_url

      const list = featuresList.value
      if (list.length > 0) {
        hoverFeature(list[0])
      } else {
        activeFeatureTitle.value = 'Overview'
        activeDesc.value = project.value.tagline || ''
      }
    }
  } catch (err) {
    console.error('Error fetching project detail:', err)
    project.value = null
  } finally {
    loading.value = false

    // Trigger GSAP entrance animations
    if (project.value) {
      nextTick(() => {
        animateEntrance()
      })
    }
  }
}

// GSAP Animations
const animateEntrance = () => {
  const tl = gsap.timeline({ defaults: { ease: 'power3.out' } })

  // Left side image and desc
  tl.fromTo('.detail-left', { opacity: 0, x: -40 }, { opacity: 1, x: 0, duration: 1 }, 0.1)

  // Right side titles
  tl.fromTo(
    '.detail-right > div:first-child',
    { opacity: 0, y: 30 },
    { opacity: 1, y: 0, duration: 0.8 },
    0.2,
  )

  // Specs table
  tl.fromTo(
    '.detail-right > div:nth-child(2)',
    { opacity: 0, scaleY: 0, transformOrigin: 'top' },
    { opacity: 1, scaleY: 1, duration: 0.6 },
    0.3,
  )

  // Description
  tl.fromTo(
    '.detail-right > div:nth-child(3)',
    { opacity: 0, y: 20 },
    { opacity: 1, y: 0, duration: 0.6 },
    0.4,
  )

  // Feature cards stagger
  const cards = document.querySelectorAll('.detail-right .group')
  if (cards.length > 0) {
    tl.fromTo(cards, { opacity: 0, y: 15 }, { opacity: 1, y: 0, stagger: 0.08, duration: 0.6 }, 0.5)
  }

  // Tech tags and links
  const rest = document.querySelectorAll(
    '.detail-right > div:nth-child(5), .detail-right > div:last-child',
  )
  if (rest.length > 0) {
    tl.fromTo(rest, { opacity: 0, y: 20 }, { opacity: 1, y: 0, stagger: 0.1, duration: 0.6 }, 0.6)
  }
}

onMounted(() => {
  fetchProjectDetails()
})
</script>

<style scoped>
/* Image crossfade animations */
.image-fade-enter-active,
.image-fade-leave-active {
  transition:
    opacity 0.4s cubic-bezier(0.16, 1, 0.3, 1),
    transform 0.4s cubic-bezier(0.16, 1, 0.3, 1);
}

.image-fade-enter-from {
  opacity: 0;
  transform: scale(1.02);
}

.image-fade-leave-to {
  opacity: 0;
  transform: scale(0.98);
}
</style>
