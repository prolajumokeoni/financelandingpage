<template>
  <div>
    <div class="relative z-[1]">

   <Navigation />
     <HeroSection />
     <FeatureCard />
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

let tabTimer

onMounted(() => {
  tabTimer = setInterval(() => { activeTab.value = (activeTab.value + 1) % whyItems.length }, 6000)
  requestAnimationFrame(() => {
    if (disclaimerEl.value) disclaimerH.value = disclaimerEl.value.offsetHeight
  })
})
onUnmounted(() => {
  clearInterval(tabTimer)
})
</script>
 