<template>
  <section class="bg-white pt-20 pb-[100px]">
    <div class="container">
      <div class="grid grid-cols-3 gap-6 max-[991px]:grid-cols-2 max-[599px]:grid-cols-1">

        <div v-for="card in cards" :key="card.title"
          class="bg-[#ECEFF1] rounded-[30px] py-10 px-[30px] flex flex-col"
        >
          <div class="w-16 h-16 rounded-[14px] flex items-center justify-center mb-6 shrink-0">
            <img :src="card.icon" class="w-[50px] h-[50px] object-contain" :alt="card.title" />
          </div>
          <h5 class="text-[18px] font-bold text-black mb-3.5 leading-[1.3]">{{ card.title }}</h5>
          <p class="text-[16px] font-medium leading-[30px] text-[#444] flex-1 mb-7">{{ card.desc }}</p>
          <a href="#" class="group flex items-center justify-between text-[15px] font-semibold text-[#1f2334] no-underline mt-auto">
            <span class="transition-colors duration-200 group-hover:text-[#44C486]">Learn more</span>
            <span class="w-9 h-9 rounded-full bg-[#d0d8dc] flex items-center justify-center transition-[background,color] duration-300 group-hover:bg-[#44C486] group-hover:text-white">
              <svg class="w-[18px] h-[22px] transition-transform duration-300 group-hover:-rotate-45" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5">
                <path d="M5 12h14M12 5l7 7-7 7" stroke-linecap="round" stroke-linejoin="round"/>
              </svg>
            </span>
          </a>
        </div>

      </div>
    </div>
  </section>
</template>

<script setup>
import featureOne from '~/assets/images/hero/futureone.svg'
import featureTwo from '~/assets/images/hero/feature2.svg'
import featureThree from '~/assets/images/hero/featurethree.svg'

const cards = [
  {
    icon: featureOne,
    title: 'Used advanced technologies',
    desc: 'I must explain to you how all this mistaken. Idea of main denouncing pleasure and praising pain was born',
  },
  {
    icon: featureTwo,
    title: 'Clean design & Typography',
    desc: 'I must explain to you how all this mistaken. Idea of main denouncing pleasure and praising pain was born',
  },
  {
    icon: featureThree,
    title: 'Best customer support',
    desc: 'I must explain to you how all this mistaken. Idea of main denouncing pleasure and praising pain was born',
  },
]
</script>
