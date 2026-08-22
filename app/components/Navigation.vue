<template>
  <!-- header is always transparent — the inner container handles the background -->
  <header class="fixed top-0 left-0 w-full z-[9999]">
    <!-- shape/width via :style so arbitrary values are always resolved at runtime -->
    <div
      class="mx-auto h-[80px] flex items-center "
      :style="isSticky
        ? { width: '100%', borderRadius: '0', marginTop: '0', paddingInline: 'calc(7.5% + 15px)' }
        : { width: '85%', borderRadius: '40px', marginTop: '20px', paddingInline: '15px' }"
      :class="isSticky
        ? 'bg-white/60 shadow-[0_10px_15px_rgba(0,0,0,0.05)] backdrop-blur-[10px]'
        : 'bg-white/10 backdrop-blur-[2.5px]'"
    >

      <!-- Logo — switches to dark version on scroll -->
      <a href="#" class="shrink-0 no-underline">
        <img
          :src="isSticky ? logoScroll : logoDefault"
          alt="Staco"
          class="h-9 w-auto"
        />
      </a>

      <!-- Nav links -->
      <div class="flex items-center ml-8 max-[991px]:hidden">
        <ul
          ref="navEl"
          role="tablist"
          aria-label="Main navigation"
          class="flex items-center list-none m-0 p-0 relative"
          @mouseleave="onLeave"
          @keydown="onKey"
        >
          <span
            aria-hidden="true"
            class="absolute top-1/2 left-0 h-9 rounded-[30px] pointer-events-none bg-white"
            :class="[ready ? 'nav-slide' : 'opacity-0', isSticky ? 'shadow-[0_1px_8px_rgba(0,0,0,0.15)]' : 'shadow-[0_2px_14px_rgba(0,0,0,0.45)]']"
            :style="{ width: pillW + 'px', transform: `translateX(${pillX}px) translateY(-50%)` }"
          ></span>

          <li
            v-for="(item, i) in navItems" :key="item"
            role="tab"
            :tabindex="i === activeIdx ? 0 : -1"
            :aria-selected="i === activeIdx"
            class="cursor-pointer rounded-[30px] outline-none nav-tab transition-colors duration-100"
            :class="isSticky ? 'hover:bg-black/[0.06]' : 'hover:bg-white/[0.12]'"
            @mouseenter="onHover($event, i)"
            @click="onSelect($event, i)"
          >
            <span
              class="flex items-center gap-1 px-4 py-[7px] text-[15px] whitespace-nowrap relative z-10 select-none transition-colors duration-150"
              :class="i === activeIdx ? 'font-bold text-[#1a1a1a]'
                : i === targetIdx ? 'font-semibold text-[#1a1a1a]'
                : isSticky ? 'font-medium text-[#1f2334]/40' : 'font-medium text-white/60'"
            >
              {{ item }}
              <svg v-if="item === 'Home' || item === 'Pages'" class="w-2.5 h-[6px] shrink-0 ml-0.5" viewBox="0 0 10 6" fill="none">
                <path d="M1 1l4 4 4-4" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
              </svg>
            </span>
          </li>
        </ul>
      </div>

      <!-- Spacer -->
      <div class="flex-1 max-[991px]:hidden"></div>

      <!-- Right actions — EN + Sign in + Start Free -->
      <div class="flex items-center gap-1 max-[991px]:hidden">
        <!-- EN -->
        <a href="#" class="flex items-center gap-1.5 text-sm font-medium px-3 py-[7px] rounded-[30px] no-underline transition-colors duration-100"
          :class="isSticky ? 'text-[#1f2334]/60 hover:bg-black/[0.06]' : 'text-white/60 hover:bg-white/[0.12]'">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" class="w-4 h-4 shrink-0">
            <circle cx="12" cy="12" r="10"/><path d="M2 12h20M12 2a15.3 15.3 0 010 20M12 2a15.3 15.3 0 000 20"/>
          </svg>
          EN
        </a>

        <!-- Sign in -->
        <a href="#" class="text-[15px] font-semibold px-3 py-[7px] rounded-[30px] no-underline transition-colors duration-100"
          :class="isSticky ? 'text-[#1f2334]/60 hover:bg-black/[0.06]' : 'text-white/60 hover:bg-white/[0.12]'">
          Sign in
        </a>

        <!-- Start Free -->
        <a href="#" class="h-9 px-5 bg-[#B2EDA1] text-[#1f2334] text-sm font-bold rounded-full flex items-center whitespace-nowrap no-underline transition-[background,color] duration-200 hover:bg-[#44C486] hover:text-white">
          Start Free
        </a>
      </div>

      <!-- Mobile burger -->
      <button
        class="hidden max-[991px]:flex items-center justify-center bg-transparent border-0 cursor-pointer w-8 h-8 p-0 transition-colors duration-300 ml-auto"
        :class="isSticky ? 'text-[#1f2334]' : 'text-white'"
        @click="mobileOpen = !mobileOpen"
      >
        <svg v-if="!mobileOpen" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" class="w-6 h-6">
          <path d="M4 6h16M4 12h16M4 18h16" stroke-linecap="round"/>
        </svg>
        <svg v-else viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" class="w-6 h-6">
          <path d="M6 18L18 6M6 6l12 12" stroke-linecap="round"/>
        </svg>
      </button>
    </div>

    <!-- Mobile dropdown -->
    <div v-if="mobileOpen" class="bg-white rounded-2xl p-4 mx-5 mb-3 shadow-[0_8px_30px_rgba(0,0,0,0.12)] flex flex-col gap-0.5">
      <a v-for="item in navItems" :key="item" href="#"
        class="px-3 py-2.5 text-[15px] font-medium text-[#1f2334] rounded-lg hover:bg-gray-50 no-underline">
        {{ item }}
      </a>
      <div class="flex gap-3 px-3 pt-2.5 items-center">
        <a href="#" class="text-[15px] font-semibold text-[#1f2334] no-underline">Sign in</a>
        <a href="#" class="h-10 px-6 bg-[#B2EDA1] text-[#1f2334] text-sm font-bold rounded-full flex items-center transition-colors hover:bg-[#44C486] hover:text-white no-underline">Start Free</a>
      </div>
    </div>
  </header>
</template>

<script setup>
import logoDefault from '~/assets/images/icons/logo.svg'
import logoScroll  from '~/assets/images/icons/logoscroll.png'
// ── State ────────────────────────────────────────────────────────────────────
const isSticky  = ref(false)
const mobileOpen = ref(false)
const navItems  = ['Home', 'Pages', 'Services', 'Blogs', 'Contact Us']
const activeIdx = ref(0)
const hoverIdx  = ref(null)
// whichever item is hovered takes priority; falls back to the active one
const targetIdx = computed(() => hoverIdx.value ?? activeIdx.value)

// ── Sliding pill indicator ───────────────────────────────────────────────────
// pillX / pillW track the left position and width of the white sliding pill
const navEl = ref(null)
const pillX = ref(0)
const pillW = ref(0)
const ready = ref(false)

// measure the bounding box of any nav item element
const measure = (el) => {
  if (!el || !navEl.value) return
  pillX.value = el.getBoundingClientRect().left - navEl.value.getBoundingClientRect().left
  pillW.value = el.getBoundingClientRect().width
}

// shortcut: measure by index instead of element
const measureAt = (i) => measure(navEl.value?.querySelectorAll('[role="tab"]')[i])

// ── Nav item event handlers ──────────────────────────────────────────────────
const onHover  = (e, i) => { hoverIdx.value = i; measure(e.currentTarget) }
const onLeave  = ()     => { hoverIdx.value = null; measureAt(activeIdx.value) }
const onSelect = (e, i) => { activeIdx.value = i; hoverIdx.value = null; measure(e.currentTarget) }

// keyboard arrow navigation (accessibility)
const onKey = (e) => {
  const n = navItems.length
  const next = { ArrowRight: (activeIdx.value + 1) % n, ArrowLeft: (activeIdx.value - 1 + n) % n, Home: 0, End: n - 1 }
  if (!(e.key in next)) return
  e.preventDefault()
  activeIdx.value = next[e.key]
  measureAt(activeIdx.value)
  navEl.value?.querySelectorAll('[role="tab"]')[activeIdx.value]?.focus()
}

// ── Scroll & resize ──────────────────────────────────────────────────────────
const onScroll = () => isSticky.value = scrollY > 60

onMounted(async () => {
  window.addEventListener('scroll', onScroll, { passive: true })
  await nextTick()
  measureAt(0)
  await nextTick()
  // delay enabling the CSS transition so it doesn't animate on first paint
  requestAnimationFrame(() => ready.value = true)
  new ResizeObserver(() => measureAt(activeIdx.value)).observe(navEl.value)
})

onUnmounted(() => window.removeEventListener('scroll', onScroll))
</script>

<style scoped>
.nav-slide {
  opacity: 1;
  transition: transform 0.38s cubic-bezier(0.34, 1.4, 0.64, 1), width 0.38s cubic-bezier(0.34, 1.4, 0.64, 1);
}
.nav-tab:focus-visible {
  box-shadow: 0 0 0 2px #44C486;
}
</style>
