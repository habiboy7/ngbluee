<template>
  <!-- Header Contact Links -->
  <div
    class="w-full px-4 sm:px-6 lg:px-12 mt-20 md:mt-32 lg:mt-40 flex flex-col md:flex-row justify-between items-start md:items-center gap-4 md:gap-6 font-mono text-xs md:text-sm lg:text-base uppercase tracking-widest z-10 relative"
  >
    <div class="flex flex-col gap-2">
      <span class="font-semibold text-gray-900">Available for collaboration</span>
      <a href="mailto:habiboy0607@gmail.com" class="group flex items-center gap-2">
        <span
          class="border-b border-gray-700 pb-0.5 group-hover:border-black transition-colors text-gray-900"
          >habiboy0607@gmail.com</span
        >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
          class="w-6 h-6 transform rotate-45 group-hover:rotate-0 transition-transform duration-300 text-gray-900"
        >
          <line x1="7" y1="17" x2="17" y2="7"></line>
          <polyline points="7 7 17 7 17 17"></polyline>
        </svg>
      </a>
    </div>

    <!-- LinkedIn-->
    <div class="flex flex-col gap-2 md:text-right md:items-end">
      <span class="font-semibold text-gray-900">Recent Work</span>
      <a
        href="https://www.linkedin.com/in/muhammadkhoerulhabibi/"
        class="group flex items-center gap-2"
        target="blank"
      >
        <span
          class="border-b border-gray-700 pb-0.5 group-hover:border-black transition-colors text-gray-900"
          >LinkedIn Profile</span
        >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
          class="w-6 h-6 transform rotate-45 group-hover:rotate-0 transition-transform duration-300 text-gray-900"
        >
          <line x1="7" y1="17" x2="17" y2="7"></line>
          <polyline points="7 7 17 7 17 17"></polyline>
        </svg>
      </a>
    </div>
  </div>

  <!-- Main Title Area -->
  <div class="title mt-12 sm:mt-6 lg:mt-16 relative z-10">
    <h2
      id="about"
      ref="aboutTitle"
      class="about-title text-center font-extrabold font-sofia text-[12vw] lg:text-[8rem] tracking-[-0.07em] leading-none text-gray-900"
    >
      ESSENCE
    </h2>
  </div>

  <!-- Content Area  -->
  <section
    ref="sectionRef"
    class="about-section w-full relative mt-8 lg:mt-16 lg:mb-20 flex justify-center"
  >
    <div ref="cardRef" class="bg-transparent text-white relative mx-auto w-full rounded-none">
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 lg:gap-6">
        <!-- About Me Profile (Top Left, Spans 2 Cols) -->
        <div
          class="col-span-1 md:col-span-2 lg:col-span-2 bg-black text-white border border-white/50 rounded-lg p-6 sm:p-10 flex flex-col justify-between hover:border-neutral-700 transition-all duration-300 group shadow-xl shadow-black/5"
        >
          <div>
            <h3
              class="font-sofia font-extrabold text-[2rem] xs:text-[2.8rem] sm:text-[3.5rem] lg:text-[4rem] leading-none text-white tracking-tighter mt-2 mb-6 uppercase"
            >
              About Me
            </h3>
          </div>

          <p
            class="reveal-text text-xs sm:text-sm lg:text-lg text-white/80 leading-relaxed font-manrope text-left lg:text-justify mt-4"
          >
            I’m <span class="font-black text-white">Muhammad Khoerul Habibi</span>, a Web Developer
            and UI/UX Designer based in Yogyakarta. I specialize in creating modern digital
            experiences through clean design and scalable web solutions. With a strong foundation in
            frontend and backend development, I focus on building fast, responsive, and
            user-centered applications that not only look great but also solve real-world problems.
          </p>
        </div>

        <!-- Core Tech Stack (Top Right, Spans 1 Col) -->
        <div
          class="col-span-1 bg-neutral-950 text-white border border-neutral-800/80 rounded-lg p-6 sm:p-8 flex flex-col justify-between hover:border-neutral-700 transition-all duration-300 group shadow-xl shadow-black/5"
        >
          <div>
            <h4
              class="font-sofia font-bold text-[2rem] sm:text-[2.8rem] lg:text-[3rem] uppercase text-white mt-1 mb-4 tracking-tight text-center"
            >
              Core Tech Stack
            </h4>

            <div class="flex flex-wrap gap-1.5 sm:gap-2 mt-2 justify-center">
              <span
                v-for="(skill, index) in skills"
                :key="index"
                class="skill-tag font-manrope px-2 py-1 sm:px-3 sm:py-1 border border-white/15 rounded-full text-base lg:text-base text-white/90 hover:bg-white hover:text-black transition-all duration-300 cursor-default backdrop-blur-sm"
              >
                {{ skill }}
              </span>
            </div>
          </div>
        </div>

        <!-- Hire Me CV Button (Bottom Left, Spans 1 Col) -->
        <div
          class="col-span-1 bg-neutral-950 text-white border border-neutral-800/80 rounded-lg p-6 sm:p-8 flex flex-col justify-between hover:border-neutral-700 transition-all duration-300 group shadow-xl shadow-black/5"
        >
          <div>
            <h4
              class="font-sofia uppercase font-bold text-[2rem] lg:text-[3rem] text-white mt-2 mb-24 lg:mb-50 tracking-tight text-center leading-none"
            >
              Let's Work Together
            </h4>

            <!-- Elegant Radar Visual  -->
            <div class="flex items-center justify-center gap-1.5">
              <div class="relative flex items-center justify-center w-8 h-8">
                <!-- Large pulsing radar rings -->
                <span
                  class="animate-ping absolute inline-flex h-8 w-8 rounded-full bg-emerald-400/30 opacity-75"
                ></span>
                <span
                  class="animate-ping absolute inline-flex h-16 w-16 rounded-full bg-emerald-500/20 opacity-40"
                  style="animation-delay: 0.5s"
                ></span>
                <!-- Solid inner dot -->
                <span
                  class="relative inline-flex rounded-full h-3.5 w-3.5 bg-emerald-500 shadow-[0_0_12px_rgba(16,185,129,0.8)]"
                ></span>
              </div>
              <span class="text-sm font-manrope tracking-widest text-emerald-400 font-semibold"
                >Available for Projects</span
              >
            </div>
          </div>

          <!-- CV Button at the bottom -->
          <div class="flex justify-center mt-6">
            <a
              href="https://drive.google.com/file/d/1neWSF-t7mZfBjjaEo_O3kXsiyhJpMtJ-/view?usp=sharing"
              target="_blank"
              rel="noopener noreferrer"
              class="group/btn relative inline-flex items-center justify-center gap-2 px-16 py-2.5 bg-white rounded-full text-xs sm:text-base text-black shadow-lg hover:scale-[1.02] hover:bg-black hover:text-white border hover:border-white transition-all duration-300 w-fit"
            >
              <span class="relative z-10 font-extrabold font-manrope">View CV</span>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2.5"
                stroke-linecap="round"
                stroke-linejoin="round"
                class="w-4 h-4 transform group-hover/btn:translate-y-[2px] transition-transform duration-300"
              >
                <path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"></path>
                <polyline points="7 10 12 15 17 10"></polyline>
                <line x1="12" y1="15" x2="12" y2="3"></line>
              </svg>
            </a>
          </div>
        </div>

        <!-- My Services (Bottom Right, Spans 2 Cols) -->
        <div
          class="col-span-1 md:col-span-2 lg:col-span-2 bg-neutral-950 text-white border border-neutral-800/80 rounded-lg p-6 sm:p-10 flex flex-col justify-between hover:border-neutral-700 transition-all duration-300 group shadow-xl shadow-black/5"
        >
          <div>
            <h4
              class="font-sofia font-bold text-[2rem] lg:text-[3rem] text-white uppercase mb-4 tracking-tight"
            >
              My Services
            </h4>

            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 mt-6">
              <!-- Web Dev -->
              <div
                class="p-6 bg-white/[0.02] border border-white/20 rounded-md hover:border-white/50 transition-colors duration-300"
              >
                <div class="flex items-center gap-3 mb-2">
                  <p class="font-manrope font-bold text-sm lg:text-xl uppercase text-white">S-01</p>
                  <h5 class="font-manrope font-bold text-sm lg:text-xl text-white">
                    Web Development
                  </h5>
                </div>
                <p class="text-xs lg:text-sm text-white/60 font-manrope text-justify">
                  Building scalable and high-performance web applications with modern technologies
                  and clean architecture.
                </p>
              </div>

              <!-- UI/UX -->
              <div
                class="p-6 bg-white/[0.02] border border-white/20 rounded-md hover:border-white/50 transition-colors duration-300"
              >
                <div class="flex items-center gap-3 mb-2">
                  <p class="font-manrope font-bold text-sm lg:text-xl uppercase text-white">S-02</p>
                  <h5 class="font-manrope font-bold text-sm lg:text-xl text-white">UI/UX Design</h5>
                </div>
                <p class="text-xs lg:text-sm text-white/60 font-manrope">
                  Designing intuitive digital experiences that balance usability, consistency, and
                  visual appeal.
                </p>
              </div>

              <!-- Mobile Dev -->
              <div
                class="p-6 bg-white/[0.02] border border-white/20 rounded-md hover:border-white/50 transition-colors duration-300"
              >
                <div class="flex items-center gap-3 mb-2">
                  <p class="font-manrope font-bold text-sm lg:text-xl uppercase text-white">S-03</p>
                  <h5 class="font-manrope font-bold text-sm lg:text-xl text-white">
                    Mobile Development
                  </h5>
                </div>
                <p class="text-xs lg:text-sm text-white/60 font-manrope">
                  Creating responsive and interactive interfaces that deliver seamless user
                  experiences across devices.
                </p>
              </div>

              <!-- Academic Work -->
              <div
                class="p-6 bg-white/[0.02] border border-white/20 rounded-md hover:border-white/50 transition-colors duration-300"
              >
                <div class="flex items-center gap-3 mb-2">
                  <p class="font-manrope font-bold text-sm lg:text-xl uppercase text-white">S-04</p>
                  <h5 class="font-manrope font-bold text-sm lg:text-xl text-white">
                    Academic Work
                  </h5>
                </div>
                <p class="text-xs lg:text-sm text-white/60 font-manrope">
                  Solving complex computer science tasks, coding homework, and software projects.
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import gsap from 'gsap'
import ScrollTrigger from 'gsap/ScrollTrigger'
import SplitType from 'split-type'

gsap.registerPlugin(ScrollTrigger)

const sectionRef = ref(null)
const cardRef = ref(null)

const skills = ref([
  'PHP',
  'Laravel',
  'Vue',
  'Tailwind CSS',
  'Bootstrap',
  'JavaScript',
  'GSAP',
  'Node Js',
  'Figma',
  'UI/UX Design',
  'Git',
  'Postman',
  'MySQL',
  'Laragon',
])

onMounted(() => {
  const title = new SplitType('.about-title', {
    types: 'chars',
  })

  gsap.set(title.chars, {
    yPercent: -120,
    opacity: 0,
  })

  // Title Scroll Trigger
  gsap
    .timeline({
      scrollTrigger: {
        trigger: '.about-title',
        start: 'top 80%',
        end: 'top 30%',
        scrub: 1,
      },
    })
    .to(title.chars, {
      yPercent: 0,
      opacity: 1,
      ease: 'power4.out',
      stagger: {
        each: 0.05,
        from: 'center',
      },
    })

  // Background Scroll Effect
  if (cardRef.value && sectionRef.value) {
    const mm = gsap.matchMedia()

    mm.add('(min-width: 1024px)', () => {
      gsap.fromTo(
        cardRef.value,
        {
          width: '100%',
          borderRadius: '0px',
        },
        {
          scrollTrigger: {
            trigger: sectionRef.value,
            start: 'top 90%',
            end: 'top 35%',
            scrub: 1,
          },
          width: 'calc(100% - 12rem)',
          borderRadius: '3.5rem',
          ease: 'none',
        },
      )
    })

    mm.add('(min-width: 640px) and (max-width: 1023px)', () => {
      gsap.fromTo(
        cardRef.value,
        {
          width: '100%',
          borderRadius: '0px',
        },
        {
          scrollTrigger: {
            trigger: sectionRef.value,
            start: 'top 90%',
            end: 'top 35%',
            scrub: 1,
          },
          width: 'calc(100% - 3rem)',
          borderRadius: '2rem',
          ease: 'none',
        },
      )
    })

    mm.add('(max-width: 639px)', () => {
      gsap.fromTo(
        cardRef.value,
        {
          width: '100%',
          borderRadius: '0px',
        },
        {
          scrollTrigger: {
            trigger: sectionRef.value,
            start: 'top 90%',
            end: 'top 35%',
            scrub: 1,
          },
          width: 'calc(100% - 1.5rem)',
          borderRadius: '1.5rem',
          ease: 'none',
        },
      )
    })
  }

  // Text Reveal Effect
  if (sectionRef.value) {
    const revealElements = sectionRef.value.querySelectorAll('.reveal-text')

    revealElements.forEach((element) => {
      const split = new SplitType(element, { types: 'words' })

      gsap.set(split.words, {
        color: '#ffffff',
        opacity: 0.25,
      })

      gsap.to(split.words, {
        scrollTrigger: {
          trigger: element,
          start: 'top 85%',
          end: 'bottom 60%',
          scrub: 0.3,
        },
        opacity: 1,
        stagger: 0.05,
        ease: 'none',
      })
    })
  }
})
</script>

<style scoped>
.reveal-text {
  backface-visibility: hidden;
  transform: translateZ(0);
}

.reveal-text :deep(.word) {
  display: inline !important;
}

.about-title {
  overflow: hidden;
}

.about-title .char {
  display: inline-block;
}
</style>
