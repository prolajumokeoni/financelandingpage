
<template>
  <section class="bg-[#ECF1F1] pt-[100px] pb-20">
    <div class="container">
      <div class="bg-white rounded-[30px] shadow-[0_5px_30px_rgba(0,0,0,.07)] overflow-hidden">

        <!-- Person + Quote -->
        <div class="grid grid-cols-2 max-[991px]:grid-cols-1">

          <!-- Left: arch shapes + person -->
          <div class="relative overflow-hidden min-h-[440px] bg-white">
            <!-- Dark teal crescent arc behind arch shapes -->
            <svg class="absolute top-0 left-0 pointer-events-none select-none" width="200" height="200" viewBox="0 0 200 200" fill="none" aria-hidden="true">
              <defs>
                <mask id="crescent-mask">
                  <rect width="200" height="200" fill="white"/>
                  <circle cx="50" cy="50" r="165" fill="black"/>
                </mask>
              </defs>
              <circle cx="0" cy="0" r="200" fill="#004D42" mask="url(#crescent-mask)"/>
            </svg>
            <!-- Arch shapes — anchored to bottom, fills most of panel -->
            <img :src="behindImg" class="absolute bottom-0 left-1/2 -translate-x-1/2" aria-hidden="true" />
            <!-- Person — bottom-aligned, narrower so dark teal arch stays visible -->
            <Transition name="testi-img" mode="out-in">
              <img
                :key="active"
                :src="testimonials[active].img"
                :alt="testimonials[active].name"
                class="absolute bottom-0 left-1/2 -translate-x-1/2  w-auto   object-contain object-top z-[1]"
              />
            </Transition>
          </div>

          <!-- Right: quote content -->
          <div class="pt-14 pb-12 pr-14 pl-8 flex flex-col justify-center">
            <img :src="quoteIcon" class="w-[60px] mb-7" aria-hidden="true" />
            <Transition name="testi-fade" mode="out-in">
              <div :key="active">
                <p class="text-[17px] leading-[34px] text-[#1f2334] mb-7">{{ testimonials[active].quote }}</p>
                <span class="block text-base font-bold text-[#1f2334]">{{ testimonials[active].name }}</span>
                <span class="text-sm text-[#888]">{{ testimonials[active].role }}</span>
              </div>
            </Transition>
          </div>

        </div>

        <!-- Brand logo nav with single full-width progress bar -->
        <div class="relative border-t border-black/[.06]">
          <!-- Single progress bar spanning full width -->
          <div class="absolute top-0 left-0 w-full h-[3px] overflow-hidden">
            <div :key="active" class="block h-full bg-[#44C486] testi-progress"></div>
          </div>
          <div class="grid" :style="{ gridTemplateColumns: `repeat(${testimonials.length}, 1fr)` }">
            <button
              v-for="(t, i) in testimonials"
              :key="i"
              @click="selectActive(i)"
              class="flex items-center justify-center py-7 bg-transparent border-0 cursor-pointer"
            >
              <img
                :src="t.logo"
                :alt="t.brand"
                class="h-7 max-w-[90px] object-contain transition-opacity duration-300"
                :class="active === i ? 'opacity-100' : 'opacity-35'"
              />
            </button>
          </div>
        </div>

      </div>
    </div>
  </section>
</template>

<script setup>
import behindImg  from '~/assets/images/progress/behindimage.svg'
import quoteIcon  from '~/assets/images/progress/download (7).svg'

import firstImg   from '~/assets/images/progress/firstprogress.png'
import secondImg  from '~/assets/images/progress/secondprogress.png'
import thirdImg   from '~/assets/images/progress/thirdprogress.png'
import fourthImg  from '~/assets/images/progress/fourthprogress.png'
import fifthImg   from '~/assets/images/progress/fifthprogress.png'

import jqueryLogo from '~/assets/images/progress/jquery.png'
import githubLogo from '~/assets/images/progress/github.png'
import portisLogo from '~/assets/images/progress/portis.png'
import envatoLogo from '~/assets/images/progress/envato.png'
import daomakLogo from '~/assets/images/progress/daomak.png'

const testimonials = [
  {
    quote: 'Very denounce with righteous indignation and dislike men who are so beguiled and demoralized by the charms of pleasure of the moment, combined with a handful so blinded by desire.',
    name: 'Peter Leo,',
    role: 'CTO – Criston',
    img: firstImg,
    logo: jqueryLogo,
    brand: 'jQuery',
  },
  {
    quote: 'I must explain to you how all this mistaken idea of denouncing pleasure and praising pain was born and I will give you a complete account of the system.',
    name: 'Roe Smith,',
    role: 'Director, Growth Marketing',
    img: secondImg,
    logo: githubLogo,
    brand: 'GitHub',
  },
  {
    quote: 'We use as filler text for layouts, non-readability is of great importance but because those who do not know how to pleasure rationally encounter consequences that are pleasure rationally encounter ❤️ ❤️',
    name: 'Aurthoe De,',
    role: 'CEO – Dorid Co',
    img: thirdImg,
    logo: portisLogo,
    brand: 'Portis',
  },
  {
    quote: 'Making this the first true 😍 generator on the Internet. It uses a dictionary of over words, combined with a handful of model sentence structures, to generate 👏👏',
    name: 'Dennis Lail,',
    role: 'Marketer',
    img: fourthImg,
    logo: envatoLogo,
    brand: 'envato',
  },
  {
    quote: 'I must explain to you how all this mistaken. Tdea of denouncing pleasure and praising pain was born and I will give you a complete account. 😍',
    name: 'Roe Smith',
    role: 'Director, Growth Marketing',
    img: fifthImg,
    logo: daomakLogo,
    brand: 'daomak',
  },
]

const active = ref(0)
let timer

const selectActive = (i) => {
  active.value = i
  clearInterval(timer)
  timer = setInterval(advance, 6000)
}

const advance = () => { active.value = (active.value + 1) % testimonials.length }

onMounted(() => { timer = setInterval(advance, 6000) })
onUnmounted(() => clearInterval(timer))
</script>

<style scoped>
.testi-fade-enter-active, .testi-fade-leave-active { transition: opacity .4s; }
.testi-fade-enter-from, .testi-fade-leave-to { opacity: 0; }

.testi-img-enter-active, .testi-img-leave-active { transition: opacity .35s, transform .35s; }

@keyframes testiProgress { from { transform: scaleX(0) } to { transform: scaleX(1) } }
.testi-progress {
  animation: testiProgress 10s linear forwards;
  transform-origin: left center;
}
</style>
