<template>
  <div>
      <!-- ─────────────── SCROLL PROGRESS ─────────────── -->
    <div class="fixed top-0 left-0 right-0 h-[3px] z-[200] pointer-events-none overflow-hidden">
      <div class="h-full bg-[#44C486]" :style="{ width: scrollProgress + '%' }"></div>
    </div>

    <!-- ─────────────── SCROLL TO TOP ─────────────── -->
    <Transition name="fade">
      <button
        v-if="scrollProgress > 2"
        @click="window.scrollTo({ top: 0, behavior: 'smooth' })"
        class="fixed bottom-8 right-6 z-[200] w-14 h-14 flex items-center justify-center cursor-pointer border-0 bg-transparent p-0"
        aria-label="Scroll to top"
      >
        <!-- Circular progress ring -->
        <svg class="absolute inset-0 z-0" width="56" height="56" viewBox="0 0 56 56" fill="none">
          <!-- Track -->
          <circle cx="28" cy="28" r="23" stroke="rgba(13,172,129,0.15)" stroke-width="3" transform="rotate(-90 28 28)"/>
          <!-- Fill -->
          <circle
            cx="28" cy="28" r="23"
            stroke="rgba(13,172,129,0.8)" stroke-width="3"
            stroke-linecap="round"
            transform="rotate(-90 28 28)"
            :stroke-dasharray="144.5"
            :stroke-dashoffset="144.5 * (1 - scrollProgress / 100)"
            style="transition: stroke-dashoffset 0.1s linear;"
          />
        </svg>
        <!-- Arrow -->
        <svg class="relative z-[1]" stroke="rgba(13,172,129,0.8)" fill="rgba(13,172,129,0.8)" stroke-width="0" viewBox="0 0 384 512" height="18" width="18" xmlns="http://www.w3.org/2000/svg">
          <path d="M214.6 41.4c-12.5-12.5-32.8-12.5-45.3 0l-160 160c-12.5 12.5-12.5 32.8 0 45.3s32.8 12.5 45.3 0L160 141.2 160 448c0 17.7 14.3 32 32 32s32-14.3 32-32l0-306.7L329.4 246.6c12.5 12.5 32.8 12.5 45.3 0s12.5-32.8 0-45.3l-160-160z"/>
        </svg>
      </button>
    </Transition>
    <div class="relative z-[1]">

   <Navigation />
     <HeroSection />
     <FeatureCard />
     <CtaSection />
     <WhyChooseUs />
     <TestimonialSection />
      <FooterSection />

      <!-- Transparent spacer — lets fixed disclaimer show through at the very bottom -->
      <div :style="{ height: disclaimerH + 'px' }"></div>

    </div> 
          <!-- ─────────────── DISCLAIMER ─────────────── -->
    <section ref="disclaimerEl" style="position:fixed;bottom:0;left:0;width:100%;z-index:0;padding:53px 0 60px;background-color:#ecf1f1;">
      <div class="container">
        <h6 style="font-weight:700;margin-bottom:11px;">Disclaimer:</h6>
        <p style="font-size:14px;margin-bottom:20px;" class="leading-6 text-[#777]">There are many variations of passages of Lorem Ipsum available, but the majority have suffered alteration in some form, by injected humour, or randomised words which don't look even slightly believable. If you are going to use a passage of Lorem Ipsum, you need to be sure there isn't anything embarrassing hidden in the middle of text. All the Lorem Ipsum generators on the Internet tend to repeat predefined chunks as necessary.</p>
        <p style="font-size:14px;" class="leading-6 text-[#777]">Making this the first true generator on the Internet. It uses a dictionary of over 200 Latin words, combined handful of model sentence structures, to generate Lorem Ipsum which looks reasonable.</p>
      </div>
    </section>

  </div>
</template>
<script setup>
useHead({
  link: [
    { rel: 'preconnect', href: 'https://fonts.googleapis.com' },
    { rel: 'preconnect', href: 'https://fonts.gstatic.com', crossorigin: '' },
    { rel: 'stylesheet', href: 'https://fonts.googleapis.com/css2?family=DM+Sans:ital,opsz,wght@0,9..40,400;0,9..40,500;0,9..40,700;0,9..40,800;1,9..40,400&display=swap' }
  ]
})

const disclaimerEl = ref(null)
const disclaimerH = ref(0)
const scrollProgress = ref(0)

const updateScroll = () => {
  const max = document.documentElement.scrollHeight - window.innerHeight
  scrollProgress.value = max > 0 ? (window.scrollY / max) * 100 : 0
}

onMounted(() => {
  requestAnimationFrame(() => {
    if (disclaimerEl.value) disclaimerH.value = disclaimerEl.value.offsetHeight
  })
  window.addEventListener('scroll', updateScroll, { passive: true })
})

onUnmounted(() => window.removeEventListener('scroll', updateScroll))
</script>
 