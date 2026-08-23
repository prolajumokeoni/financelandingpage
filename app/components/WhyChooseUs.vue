
<template>
  <section class="bg-white py-[120px]">
    <div class="container">
      <div class="grid grid-cols-2 gap-[60px] items-center max-[991px]:grid-cols-1">

        <!-- Left content -->
        <div>
          <Transition name="why-fade" mode="out-in">
            <div :key="activeTab">
              <p class="text-base font-bold text-[#44C486] tracking-[.2em] mb-3.5">WHY CHOOSE US</p>
              <h2 class="text-[42px] font-extrabold text-[#1f2334] leading-[1.25] mb-[22px]">{{ whyItems[activeTab].title }}</h2>
              <p class="text-base leading-[34px] text-[#666] mb-[30px]">{{ whyItems[activeTab].desc }}</p>
              <ul class="grid grid-cols-2 gap-3.5">
                <li v-for="c in whyItems[activeTab].checks" :key="c" class="flex items-center gap-2.5 text-[15px] font-semibold text-[#1f2334]">
                  <span class="w-[22px] h-[22px] shrink-0 text-[#44C486]">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 16" class="w-full h-full">
                      <path fill="currentColor" d="M12.736 3.97a.733.733 0 0 1 1.047 0c.286.289.29.756.01 1.05L7.88 12.01a.733.733 0 0 1-1.065.02L3.217 8.384a.757.757 0 0 1 0-1.06a.733.733 0 0 1 1.047 0l3.052 3.093l5.4-6.425z"/>
                    </svg>
                  </span>
                  {{ c }}
                </li>
              </ul>
            </div>
          </Transition>
        </div>

        <!-- Right: panel slider -->
        <div class="flex gap-3 h-[460px]">
          <div
            v-for="(item, i) in whyItems"
            :key="i"
            class="rounded-[20px] overflow-hidden relative cursor-pointer min-w-[50px]"
            :style="{ flex: activeTab === i ? '1' : '0.15', transition: 'flex .5s cubic-bezier(.4,0,.2,1)' }"
            @click="selectTab(i)"
          >
            <img :src="panelImgs[i]" :alt="item.title" class="w-full h-full object-cover" />
            <div
              class="absolute inset-0 bg-[linear-gradient(180deg,rgba(0,0,0,.1)_0%,rgba(0,0,0,.7)_100%)] transition-[opacity] duration-300"
              :class="activeTab === i ? 'opacity-30' : 'opacity-100'"
            ></div>
            <!-- Progress bar: track + animated fill -->
            <div v-if="activeTab === i" class="absolute left-[20px] right-[20px] bottom-[30px] h-[8px] rounded-[4px] overflow-hidden bg-white/20">
              <div :key="activeTab" class="block w-full h-full bg-white rounded-[4px] progress-fill"></div>
            </div>
          </div>
        </div>

      </div>
    </div>
  </section>
</template>

<script setup>
import caroselOne from '~/assets/images/carosel/caroselone.png'
import caroselTwo from '~/assets/images/carosel/caroseltwo.png'
import caroselThree from '~/assets/images/carosel/caroselthree.png'

const whyItems = [
  {
    title: 'Discover business Opportunities',
    desc: 'We use as filler text for layouts, non-readability is of great importance but because those who do not know how to pursue pleasure rationally encounter consequences that are extremely painful nor again is there anyone.',
    checks: ['Profile Consultation', 'Asset management', 'No-risk business idea'],
  },
  {
    title: 'Manage team increase productivity',
    desc: 'We use as filler text for layouts, non-readability is of great importance but because those who do not know how to pursue pleasure rationally encounter consequences that are extremely painful.',
    checks: ['99% Survey Report', 'Trusted by teams', 'Self-Service'],
  },
  {
    title: 'Build lasting financial security',
    desc: 'We use as filler text for layouts, non-readability is of great importance but because those who do not know how to pursue pleasure rationally encounter consequences that are extremely painful.',
    checks: ['Secure Transactions', 'Real-time Analytics', 'Expert Advisory'],
  }
]

const panelImgs = [caroselOne, caroselTwo, caroselThree]
const activeTab = ref(0)
let tabTimer

const selectTab = (i) => {
  activeTab.value = i
  clearInterval(tabTimer)
  tabTimer = setInterval(advance, 6000)
}

const advance = () => { activeTab.value = (activeTab.value + 1) % whyItems.length }

onMounted(() => { tabTimer = setInterval(advance, 6000) })
onUnmounted(() => clearInterval(tabTimer))
</script>

<style scoped>
.why-fade-enter-active, .why-fade-leave-active { transition: opacity .4s; }
.why-fade-enter-from, .why-fade-leave-to { opacity: 0; }

@keyframes panelProgress { from { transform: scaleX(0) } to { transform: scaleX(1) } }
.progress-fill {
  animation: panelProgress 6s linear forwards;
  transform-origin: left center;
}
</style>