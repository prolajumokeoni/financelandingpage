
<template>
  <section class="relative overflow-hidden bg-[#1f2334] pt-[247px] pb-[212px] ">

   <div class="container">
      <div class="grid grid-cols-2 gap-12 items-center max-[991px]:grid-cols-1 max-[991px]:gap-10">

        <!-- Left text -->
      <div>
          <h1 class="text-[60px] text-[42px] font-extrabold text-white leading-[1.46] mb-[22px] tracking-[-0.5px]">
            Financial Security<br>
            Made
            <span class="inline-grid align-bottom [&>*]:[grid-column:1] [&>*]:[grid-row:1]">
              <!-- ghost of longest word locks slot width — no layout shift on word transition -->
              <span class="invisible pointer-events-none text-[#B2EDA1]" aria-hidden="true">Accountable</span>
              <Transition name="word" mode="out-in">
                <span class="relative inline-block text-[#B2EDA1] justify-self-start" :key="wordIdx">
                  {{ heroWords[wordIdx] }}
                  <span class="absolute left-0 bottom-[-3px] w-full h-[8px] overflow-hidden">
                    <span class="block w-full h-full bg-[#B2EDA1]  hero-progress"></span>
                  </span>
                </span>
              </Transition>
            </span>
          </h1>

          <p class="text-[17px] font-medium leading-[34px] text-white/85 mb-[44px]">
            Staco is the dedicated platform for human management that helps<br>
            to grow your startup business quickly
          </p>

          <div class="flex items-center gap-7 flex-wrap">
            <!-- Primary CTA with sliding text animation -->
            <a href="#" class="btn-olive w-[220px] h-[60px] bg-[#44C486] hover:bg-[#B2EDA1] rounded-full flex items-center justify-center overflow-hidden relative transition-[background] duration-300">
              <span class="relative inline-block">
                <span class="btn-normal block text-base font-bold text-white">Get Start For Free</span>
                <span class="btn-hover block text-base font-bold">Get Start For Free</span>
              </span>
            </a>
              <!-- Let's talk -->
            <a href="#" class="group flex items-center gap-2 text-[15px] font-semibold text-white hover:text-[#B2EDA1] transition-colors duration-200 no-underline">
              Let's talk
              <span class="w-9 h-9 rounded-full border border-white/40 flex items-center justify-center transition-[border-color,background] duration-200 group-hover:border-none group-hover:bg-[#44c486]">
                <svg class="w-[14px] h-[14px] transition-transform duration-200 group-hover:-rotate-45" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5">
                  <path d="M9 18l6-6-6-6" stroke-linecap="round" stroke-linejoin="round"/>
                </svg>
              </span>
            </a>
          </div>
        </div>

      
     <!-- Right video -->
        <div class="flex justify-end  relative">
  <span class="absolute top-[-295px] left-[40px] pointer-events-none z-10 h-full max-[991px]:hidden">
            <img :src="ribbonOne"  class="w-full"/>
          </span>

          <span class="absolute -bottom-4 left-[-50px] pointer-events-none z-0 h-full max-[991px]:hidden">
            <img :src="ribbonTwo" class="w-full" />
          </span>
          <div class="w-full max-w-[470px] h-[340px] rounded-[30px] overflow-hidden relative">
            <video
              ref="videoEl"
              src="./../assets/video/herovideo.mp4"
              class="w-full h-full object-cover"
              playsinline
              loop
            ></video>
            <!-- gradient overlay -->
            <div class="absolute inset-0 bg-[linear-gradient(117.62deg,rgba(0,0,0,0)_51.24%,rgb(0,0,0)_100%)] z-[1]"></div>
            <button
              class="absolute bottom-5 right-5 z-[2] w-12 h-12 rounded-full bg-white border-0 cursor-pointer flex items-center justify-center hover:scale-105 transition-transform duration-200"
              @click="togglePlay"
            >
              <!-- Pause icon -->
              <svg v-if="isPlaying" class="w-[18px] h-[18px] fill-[#1f2334]" viewBox="0 0 24 24">
                <path d="M10 4H6v16h4V4zm8 0h-4v16h4V4z"/>
              </svg>
              <!-- Play icon -->
              <svg v-else class="w-[18px] h-[18px] fill-[#1f2334]" viewBox="0 0 24 24">
                <path d="M8 5v14l11-7L8 5z"/>
              </svg>
            </button>
            <div>
        
            </div>

          </div>

 
        </div>

      </div>
    </div>
  </section>
</template>

<script setup>

import ribbonOne from '~/assets/images/hero/ribbonone.svg'
import ribbonTwo from '~/assets/images/hero/ribbontwo.svg'

const heroWords = ['Easier', 'Accountable', 'Unbeatable']
const wordIdx = ref(0)
let wordTimer


const videoEl = ref(null)
const isPlaying = ref(false)

const togglePlay = () => {
  if (!videoEl.value) return
  if (isPlaying.value) {
    videoEl.value.pause()
  } else {
    videoEl.value.play()
  }
  isPlaying.value = !isPlaying.value
}

onMounted(() => {
  wordTimer = setInterval(() => { wordIdx.value = (wordIdx.value + 1) % heroWords.length }, 3500)
})
onUnmounted(() => clearInterval(wordTimer))
</script>


<style scoped>
/* Vue transition hooks — must be CSS class names, cannot use Tailwind */
.word-enter-active, .word-leave-active { transition: opacity .3s, transform .3s; }
.word-enter-from { opacity: 0; transform: translateY(12px); }
.word-leave-to  { opacity: 0; transform: translateY(-12px); }

/* Hero word progress bar */
@keyframes heroProgress { from { transform: scaleX(0) } to { transform: scaleX(1) } }
.hero-progress {
  animation: heroProgress 4.5s linear forwards;
  transform-origin: left center;
}

/* Button sliding text — uses translate(-50%, 80%) which has no Tailwind equivalent */
.btn-normal { transition: transform .5s cubic-bezier(.15,.85,.31,1), opacity .4s; }
.btn-olive:hover .btn-normal { transform: translateY(-150%); opacity: 0; color: #111; }
.btn-hover {
  position: absolute; width: 100%; top: 50%; left: 50%;
  transform: translate(-50%, 80%); opacity: 0;
  transition: transform .5s cubic-bezier(.15,.85,.31,1), opacity .4s;
}
.btn-olive:hover .btn-hover { transform: translate(-50%, -50%); opacity: 1; color: #111; }
</style>
