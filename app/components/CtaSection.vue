<template>
  <section ref="sectionEl" class="bg-white pb-10">
    <div class="container">
      <div class="bg-[#004D42] rounded-[30px] px-[70px] grid grid-cols-[1fr_auto] items-end overflow-hidden max-[767px]:px-[30px] max-[767px]:grid-cols-1">
        <div class="pt-14 pb-[70px]">
          <h2 class="text-[50px] font-extrabold text-white leading-[1.2] mb-[34px] max-[991px]:text-4xl">We are building<br>financial foundations</h2>
          <a href="#" class="group inline-flex items-center gap-2.5 w-[170px] h-[60px] bg-[#B2EDA1] text-[#111] text-base font-bold rounded-full justify-center no-underline transition-[background,color] duration-200 hover:bg-[#44C486] hover:text-white">
            Let's Talk
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" class="w-4 h-4 transition-transform duration-300 group-hover:-rotate-45">
              <path d="M5 12h14M12 5l7 7-7 7" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
          </a>
        </div>
        <div
          class="self-end max-[767px]:hidden"
          :style="{ transform: `translateY(${translateY}px)` }"
        >
          <img :src="arrowsSvg" alt="" width="372" height="250">
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import arrowsSvg from '~/assets/images/cta/arrows.svg'

const sectionEl = ref(null)
const translateY = ref(250)

const onScroll = () => {
  if (!sectionEl.value) return
  const rect = sectionEl.value.getBoundingClientRect()
  // progress: 0 when section bottom enters viewport, 1 when section top reaches viewport top
  const progress = Math.min(1, Math.max(0, (window.innerHeight - rect.top) / window.innerHeight))
  translateY.value = Math.round(250 - progress * 250)
}

onMounted(() => {
  onScroll()
  window.addEventListener('scroll', onScroll, { passive: true })
})
onUnmounted(() => window.removeEventListener('scroll', onScroll))
</script>
