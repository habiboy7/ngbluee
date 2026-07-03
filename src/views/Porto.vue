<template>
  <div class="relative w-full h-[160px] sm:h-[220px] md:h-[300px] overflow-hidden bg-[#f3f3f3] will-change-transform">
    <div
      class="absolute inset-0 bg-black z-0"
      style="clip-path: polygon(0 66%, 100% 14%, 100% 100%, 0% 100%)"
    ></div>
    <div
      class="absolute left-[-30%] w-[160%] rotate-[-6deg] sm:rotate-[-6deg] z-20 border-b-[3px] sm:border-b-[6px] border-white top-[46px] sm:top-[85px] md:top-[120px] bg-black"
    >
      <div class="flex whitespace-nowrap animate-[marquee-left_20s_linear_infinite]"> 
        <template v-for="n in 10" :key="n">
          <span class="flex items-center text-xs sm:text-lg md:text-2xl font-extrabold text-white py-2.5 sm:py-4 md:py-5 px-4 sm:px-6 md:px-8 font-manrope">
            We design, develop, and launch brands online
            <span class="w-1.5 h-1.5 sm:w-3 sm:h-3 bg-white rounded-full mx-3 sm:mx-6"></span>
          </span>
        </template>
      </div>
    </div>
    <div 
      class="absolute left-[-30%] w-[160%] rotate-[6deg] sm:rotate-[6deg] z-30 top-[55px] sm:top-[85px] md:top-[120px]"
    >
      <div class="flex whitespace-nowrap animate-[marquee-right_20s_linear_infinite]">
        <template v-for="n in 10" :key="n">
          <span
            class="flex items-center text-xs sm:text-lg md:text-2xl font-extrabold text-black py-2.5 sm:py-4 md:py-5 px-4 sm:px-6 md:px-8 bg-[#e9e9f2] font-manrope"
          >
            Designed with purpose — Built to perform
            <img src="/src/assets/img/star.png" class="w-4 h-4 sm:w-6 sm:h-6 mx-3 sm:mx-6" alt="star"/>
          </span>
        </template>
      </div>
    </div>
  </div>

  <!-- Showcase -->
  <section
    class="dark-zone showcase-section bg-black text-white py-24 px-4 sm:px-6 lg:px-12 relative" id="showcase"
  >
    <div class="flex flex-col sm:flex-row justify-between sm:items-end w-full mb-8 sm:mb-12 gap-4">
      <div class="title overflow-hidden">
        <h2
          class="showcase font-extrabold font-sofia text-[12vw] sm:text-[8vw] lg:text-[7rem] tracking-[-0.07em] leading-none text-white"
        >
          SHOWCASE
        </h2>
      </div>
      <div class="pb-0 sm:pb-2">
        <router-link
          to="/projects"
          class="group inline-flex items-center gap-2 rounded-full bg-white px-4 py-2 sm:px-5 sm:py-2.5 font-manrope text-sm sm:text-base font-semibold text-black hover:bg-neutral-200 transition-all duration-300 shadow-md hover:shadow-lg"
        >
          <span>More</span>
          <span
            class="inline-block w-2 h-2 rounded-full bg-black transition-transform group-hover:scale-125"
          />
        </router-link>
      </div>
    </div>

    <!-- Accordion Showcase  -->
    <div
      ref="wrapperRef"
      class="accordion-wrapper dark-zone relative -mx-4 sm:-mx-6 lg:-mx-12"
      @mouseenter="onMouseEnter"
      @mousemove="onMouseMove"
      @mouseleave="onMouseLeave"
    >
      <div
        ref="accordionRef"
        class="accordion-container lg:h-[620px] flex flex-col lg:flex-row bg-black border-t border-white select-none overflow-hidden"
      >
        <div
          v-for="(project, index) in displayProjects"
          :key="project.id"
          :ref="(el) => setItemRef(el, index)"
          @click="onClick(index)"
          class="accordion-item relative p-4 sm:p-5 lg:p-8 flex flex-col justify-between overflow-hidden bg-black cursor-pointer lg:cursor-default"
          :class="[
            activeIndex === index
              ? 'flex-[2.4] cursor-default'
              : activeIndex === null
                ? 'flex-[1]'
                : 'flex-[0.65]',
            activeIndex === index ? 'is-active-mobile' : '',
          ]"
        >
          <!-- Borders: Horizontal separator on mobile, vertical on desktop -->
          <div
            v-if="index > 0"
            class="lg:hidden absolute left-0 right-0 top-0 border-t border-white/30 pointer-events-none"
          />
          <div
            v-if="index > 0 && activeIndex !== index && activeIndex !== index - 1"
            class="hidden lg:block absolute left-0 top-0 bottom-0 border-l border-white pointer-events-none"
          />

          <!-- Desktop hook borders (hidden on mobile) -->
          <div
            v-if="activeIndex === index"
            class="hidden lg:block absolute left-0 top-0 bottom-2 border-l border-white pointer-events-none"
          />
          <div
            v-if="activeIndex === index"
            class="hidden lg:block absolute bottom-2 left-0 w-3.5 h-2 border-b border-l border-white pointer-events-none"
          />
          <div
            v-if="activeIndex === index"
            class="hidden lg:block absolute right-0 top-0 bottom-2 border-r border-white pointer-events-none"
          />
          <div
            v-if="activeIndex === index"
            class="hidden lg:block absolute bottom-2 right-0 w-3.5 h-2 border-b border-r border-white pointer-events-none"
          />

          <!-- INACTIVE STATE -->
          <div
            :ref="(el) => setInactiveRef(el, index)"
            class="inactive-state flex flex-row lg:flex-col items-center lg:items-start gap-3 lg:gap-2 pointer-events-none"
          >
            <span class="font-sofia text-sm lg:text-2xl font-semibold tracking-wider"
              >SC-{{ index + 1 }}</span
            >
            <span
              class="font-sofia font-extrabold text-base sm:text-xl lg:text-3xl text-white uppercase tracking-tighter leading-none"
            >
              {{ project.title }}
            </span>
            <!-- Mobile expand indicator -->
            <svg
              class="lg:hidden ml-auto w-4 h-4 text-neutral-500 transition-transform duration-300"
              :class="activeIndex === index ? 'rotate-180' : ''"
              fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"
            >
              <path stroke-linecap="round" stroke-linejoin="round" d="M19 9l-7 7-7-7" />
            </svg>
          </div>

          <!-- ACTIVE STATE -->
          <div
            :ref="(el) => setActiveRef(el, index)"
            class="active-state pointer-events-none opacity-0"
            :class="[
              activeIndex === index
                ? 'relative mt-4 lg:mt-0 lg:absolute lg:inset-0 lg:p-8 flex flex-col lg:justify-between'
                : 'absolute inset-0 p-4 lg:p-8 flex flex-col lg:justify-between'
            ]"
          >
            <!-- Top Row (desktop only) -->
            <div class="active-header hidden lg:flex justify-between items-start pb-4">
              <span
                class="font-sofia font-black text-4xl tracking-tighter text-white leading-none"
              >
                00-{{ index + 1 }}
              </span>
              <span
                class="font-sofia font-extrabold text-xl lg:text-3xl text-white uppercase tracking-tight flex items-center gap-2"
              >
                <span class="font-light">//</span> {{ project.title }}
              </span>
            </div>

            <!-- Content -->
            <div class="grid grid-cols-1 lg:grid-cols-12 gap-3 sm:gap-4 lg:gap-6 items-start lg:items-center flex-grow lg:py-4">
              <!-- Features -->
              <div class="lg:col-span-6 space-y-2 lg:space-y-4">
                <div
                  class="active-features-label font-manrope font-bold text-sm sm:text-base lg:text-3xl tracking-tight mb-2 lg:mb-5"
                >
                  Features
                </div>
                <div class="space-y-1.5 lg:space-y-1">
                  <div
                    v-for="(feature, fIndex) in getFeatures(project)"
                    :key="fIndex"
                    class="active-feature font-sofia font-bold text-xs sm:text-sm lg:text-lg uppercase tracking-wide flex items-center gap-2"
                  >
                    <span class="font-semibold">/</span> {{ feature }}
                  </div>
                </div>
              </div>

              <!-- Image -->
              <div class="lg:col-span-6 flex lg:justify-end justify-center">
                <div
                  class="active-image relative w-full max-w-[200px] sm:max-w-[240px] lg:max-w-[280px] aspect-[4/3] rounded-lg lg:rounded-xl overflow-hidden border border-white/10 shadow-2xl"
                >
                  <img
                    :src="project.image_url"
                    class="w-full h-full object-cover"
                    :alt="project.title"
                  />
                  <div
                    class="absolute inset-0 bg-gradient-to-t from-black/50 via-transparent to-transparent"
                  ></div>
                </div>
              </div>
            </div>

            <!-- Bottom -->
            <div
              class="active-bottom pt-3 lg:pt-4 flex flex-col sm:flex-row justify-between items-start sm:items-center gap-3 sm:gap-4"
            >
              <p class="font-manrope text-[11px] sm:text-xs max-w-lg leading-relaxed text-neutral-400">
                {{ project.tagline || project.description }}
              </p>
              <router-link
                :to="'/project/' + getSlug(project)"
                class="active-btn inline-flex items-center gap-2 px-4 py-1.5 sm:px-5 sm:py-2 rounded-full bg-white text-black text-sm sm:text-base font-manrope font-bold hover:bg-black hover:text-white hover:border border-white transition-all duration-300 shadow-md hover:shadow-lg whitespace-nowrap self-end sm:self-auto pointer-events-auto"
              >
                View Project
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2.5"
                  class="w-4 h-4 sm:w-4 sm:h-4"
                >
                  <line x1="7" y1="17" x2="17" y2="7"></line>
                  <polyline points="7 7 17 7 17 17"></polyline>
                </svg>
              </router-link>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { onMounted, onUnmounted, ref, computed, nextTick, watch } from 'vue'
import gsap from 'gsap'
import ScrollTrigger from 'gsap/ScrollTrigger'
import SplitType from 'split-type'
import { supabase } from '../lib/supabase'

gsap.registerPlugin(ScrollTrigger)

const allProjects = ref([])
const activeIndex = ref(null)
let leaveTimer = null
let revealTl = null // GSAP timeline for the active card reveal

// Template refs
const wrapperRef = ref(null)
const accordionRef = ref(null)
const itemRefs = ref([])
const inactiveRefs = ref([])
const activeRefs = ref([])

const setItemRef = (el, index) => {
  if (el) itemRefs.value[index] = el
}
const setInactiveRef = (el, index) => {
  if (el) inactiveRefs.value[index] = el
}
const setActiveRef = (el, index) => {
  if (el) activeRefs.value[index] = el
}

watch(activeIndex, (newIdx, oldIdx) => {
  if (revealTl) {
    revealTl.kill()
    revealTl = null
  }

  activeRefs.value.forEach((el) => {
    if (!el) return
    gsap.set(el, { opacity: 0, pointerEvents: 'none' })
  })
  inactiveRefs.value.forEach((el) => {
    if (!el) return
    gsap.set(el, { opacity: 1 })
  })

  if (newIdx === null) return

  const activeEl = activeRefs.value[newIdx]
  const inactiveEl = inactiveRefs.value[newIdx]
  if (!activeEl) return

  if (inactiveEl) {
    gsap.to(inactiveEl, { opacity: 0, duration: 0.25, ease: 'power2.in' })
  }

  revealTl = gsap.timeline({ defaults: { ease: 'power3.out' } })

  revealTl.to(activeEl, {
    opacity: 1,
    pointerEvents: 'auto',
    duration: 0.1,
  })

  const header = activeEl.querySelector('.active-header')
  if (header) {
    revealTl.fromTo(header, { opacity: 0, x: -30 }, { opacity: 1, x: 0, duration: 0.5 }, 0.05)
  }

  const featLabel = activeEl.querySelector('.active-features-label')
  if (featLabel) {
    revealTl.fromTo(featLabel, { opacity: 0, y: 10 }, { opacity: 1, y: 0, duration: 0.35 }, 0.15)
  }

  const features = activeEl.querySelectorAll('.active-feature')
  if (features.length) {
    revealTl.fromTo(
      features,
      { opacity: 0, x: -20 },
      { opacity: 1, x: 0, duration: 0.4, stagger: 0.07 },
      0.2,
    )
  }

  const image = activeEl.querySelector('.active-image')
  if (image) {
    revealTl.fromTo(
      image,
      { opacity: 0, clipPath: 'inset(10% 10% 10% 10%)', scale: 1.05 },
      { opacity: 1, clipPath: 'inset(0% 0% 0% 0%)', scale: 1, duration: 0.6 },
      0.15,
    )
  }

  const bottom = activeEl.querySelector('.active-bottom')
  if (bottom) {
    revealTl.fromTo(bottom, { opacity: 0, y: 15 }, { opacity: 1, y: 0, duration: 0.45 }, 0.35)
  }
})


const fetchProjects = async () => {
  try {
    const { data, error } = await supabase
      .from('projects')
      .select('*')
      .order('created_at', { ascending: false })
    if (error) throw error
    allProjects.value = data || []
  } catch (err) {
    console.error('Error fetching projects:', err)
  }
}

const displayProjects = computed(() => {
  const favorites = allProjects.value.filter((p) => p.is_favorite === true)
  const nonFavorites = allProjects.value.filter((p) => p.is_favorite !== true)
  const projects = [...favorites]

  if (projects.length < 5) {
    const spaceLeft = 5 - projects.length
    projects.push(...nonFavorites.slice(0, spaceLeft))
  }

  return projects.slice(0, 5)
})

const getFeatures = (project) => {
  if (project.features && Array.isArray(project.features) && project.features.length > 0) {
    const valid = project.features.filter((f) => f && f.trim() !== '')
    if (valid.length > 0) return valid.slice(0, 4)
  }
  return ['Interactive Experience', 'Responsive Design', 'Optimized Performance']
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

const getSlug = (project) => {
  return slugify(project.title)
}

let cachedWrapperRect = null

const onMouseEnter = () => {
  const wrapper = wrapperRef.value
  if (wrapper) {
    cachedWrapperRect = wrapper.getBoundingClientRect()
  }
}

const onMouseMove = (event) => {
  if (window.innerWidth < 1024) return

  // Cancel any pending leave timer
  if (leaveTimer) {
    clearTimeout(leaveTimer)
    leaveTimer = null
  }

  const wrapper = wrapperRef.value
  if (!wrapper) return

  if (!cachedWrapperRect) {
    cachedWrapperRect = wrapper.getBoundingClientRect()
  }

  const relativeX = event.clientX - cachedWrapperRect.left

  const N = displayProjects.value.length
  if (N === 0) return

  // Calculate dynamic boundaries based on current activeIndex
  const boundaries = []
  let accumulatedFraction = 0
  const totalFlex = activeIndex.value === null
    ? N
    : 2.4 + (N - 1) * 0.65

  for (let i = 0; i < N; i++) {
    let fraction
    if (activeIndex.value === null) {
      fraction = 1 / N
    } else if (activeIndex.value === i) {
      fraction = 2.4 / totalFlex
    } else {
      fraction = 0.65 / totalFlex
    }
    accumulatedFraction += fraction
    boundaries.push(accumulatedFraction * cachedWrapperRect.width)
  }

  // Find which column relativeX falls into
  let newIndex = 0
  for (let i = 0; i < N; i++) {
    if (relativeX <= boundaries[i]) {
      newIndex = i
      break
    }
  }

  if (activeIndex.value !== newIndex) {
    activeIndex.value = newIndex
  }
}

const onMouseLeave = () => {
  cachedWrapperRect = null
  if (window.innerWidth < 1024) return
  if (leaveTimer) clearTimeout(leaveTimer)
  leaveTimer = setTimeout(() => {
    activeIndex.value = null
    leaveTimer = null
  }, 150)
}

// Click events for mobile/tablet toggle
const onClick = (index) => {
  if (window.innerWidth < 1024) {
    activeIndex.value = activeIndex.value === index ? null : index
  }
}

onMounted(async () => {
  await fetchProjects()
  await nextTick()

  // Title Scroll Animation 
  const title = new SplitType('.showcase', { types: 'chars' })
  gsap.set(title.chars, { yPercent: -120, opacity: 0 })
  gsap
    .timeline({
      scrollTrigger: { trigger: '.showcase', start: 'top 80%', end: 'top 30%', scrub: 1 },
    })
    .to(title.chars, {
      yPercent: 0,
      opacity: 1,
      ease: 'power4.out',
      stagger: { each: 0.05, from: 'center' },
    })

  // Accordion Columns Stagger Reveal
  gsap.fromTo(
    '.accordion-item',
    { y: 50, opacity: 0 },
    {
      scrollTrigger: { trigger: '.accordion-container', start: 'top 80%' },
      y: 0,
      opacity: 1,
      duration: 0.8,
      stagger: 0.1,
      ease: 'power2.out',
    },
  )
})

onUnmounted(() => {
  if (leaveTimer) {
    clearTimeout(leaveTimer)
    leaveTimer = null
  }
  if (revealTl) {
    revealTl.kill()
    revealTl = null
  }
})
</script>

<style>
/* ANIMASI MARQUEE */
@keyframes marquee-left {
  from {
    transform: translateX(0);
  }
  to {
    transform: translateX(-50%);
  }
}
@keyframes marquee-right {
  from {
    transform: translateX(-50%);
  }
  to {
    transform: translateX(0);
  }
}

.showcase-section {
  overflow-x: clip;
}

.accordion-container {
  contain: layout style;
}

.accordion-item {
  transition:
    flex-grow 0.7s cubic-bezier(0.16, 1, 0.3, 1),
    max-height 0.7s cubic-bezier(0.16, 1, 0.3, 1);
  backface-visibility: hidden;
  -webkit-backface-visibility: hidden;
}

/* Mobile / Tablet: vertical stack accordion */
@media (max-width: 1023px) {
  .accordion-item {
    min-height: 56px;
    max-height: 56px;
    padding-top: 14px;
    padding-bottom: 14px;
  }
  .accordion-item.is-active-mobile {
    max-height: 600px;
    min-height: auto;
  }
}

/* Tablet specific tweaks */
@media (min-width: 640px) and (max-width: 1023px) {
  .accordion-item {
    min-height: 64px;
    max-height: 64px;
  }
  .accordion-item.is-active-mobile {
    max-height: 650px;
  }
}

.showcase .char {
  display: inline-block;
}
</style>
